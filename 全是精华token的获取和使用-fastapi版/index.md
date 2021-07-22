# Token的获取和使用-FastApi版


# 前言

通常，我们的接口都是需要认证后才能可以访问的，前面我们介绍了 `token` 的生成和校验，那在 `FastApi` 中怎么设计需要认证的接口呢？

# 定义令牌对象

```y
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/token/")
```

以上`/token/`为获取 `token` 的 `URI`，具体内容如下：

```py
class Token(BaseModel):
    access_token: str
    token_type: str

@app.post('/token/',response_model=Token)
async def get_token(response:Response,form_data: OAuth2PasswordRequestForm = Depends()):
    if form_data.username=='phyger' and form_data.password=='phyger666':
        response.headers['access_token']=create_token()
        return {"access_token":create_token(),"token_type":"bearer"}
```

`/token/`可以返回指定格式的令牌信息。

# 定义需要认证的接口

```py
@app.get('/format/{name}')
async def fmt(name,token=Depends(oauth2_scheme)):
    print(token)
    print(type(name))
    new_name = name.title()
    return {'result':new_name}
```

### 直接访问此接口

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/456a5dbcad24437b98fab891e3cc28a5~tplv-k3u1fbpfcp-zoom-1.image " ")

如上，直接访问会提示未认证，这样，我们已经达到了目的，但是怎么样才能实现准确无误的认证呢？

### 带上 bearer token 试试

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/380d500ce7ae42e89a18ba15b2cbf837~tplv-k3u1fbpfcp-zoom-1.image " ")

你会发现，我们携带的错误的 `token` 也能成功，这是为什么呢？

> 因为在接口中，我们通过 `oauth2_scheme` 拿到了 `token`，这个 `token` 是标准的 `bearer` 格式，但是我们没有对其进行校验，所以只要格式正确，接口都能正常返回。

### 使用错误的 bearer 格式

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fb72bf4a69c448c78491bfc78f33060b~tplv-k3u1fbpfcp-zoom-1.image " ")

如上，使用错误的 `bearer` 格式的 `token`，就无法访问接口了。

# 获取和校验 token

思路：通过上面的代码，我们将获取 `token`，校验 `token` 封装成一个静态方法，在需要认证的接口中对这个方法进行依赖即可。

### 封装的接口

```py
from utm import judge_token

def login_required(token=Depends(oauth2_scheme)):
    credentials_exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="认证失败！",
        headers={"WWW-Authenticate": "Bearer"},
    )

    if judge_token(token=token):
        return True
    else:
        raise credentials_exception
```

### 需要认证的接口

```py
@app.get('/format/{name}')
async def fmt(name,token=Depends(login_required)):
    print(token)
    print(type(name))
    new_name = name.title()
    return {'result':new_name}
```

### 直接访问/format/{name}接口

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ab29c88686094b02bf59d3a7061ee9d1~tplv-k3u1fbpfcp-zoom-1.image " ")

提示：未认证！

### 携带过期的 token 访问

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9488b269ea4a43b4a9012bc305be66b2~tplv-k3u1fbpfcp-zoom-1.image " ")

提示：认证失败！

### 使用错误 bearer 格式

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f3547e4941644bfa400381dd8607586~tplv-k3u1fbpfcp-zoom-1.image " ")

提示：未认证！

### 使用正确有效的 token

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9c2d7770755c4d788f65a88f72d00456~tplv-k3u1fbpfcp-zoom-1.image " ")

如上，成功！

> 上面，我们将 `token` 错误，`token` 过期都统一定义为认证失败！后续可以进行细化。还需要考虑 `token` 续签的实现。

