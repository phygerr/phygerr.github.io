# Token的生成和校验


# 什么是 token

`token`（也称令牌）就是一串字符，其作用是为了减轻频繁进行用户名和密码的验证而对服务器产生的压力。客户端首次访问通过正确的用户名和密码从服务端拿到 `token`，之后客户端携带 `token` 即可完成验证，无需重复携带用户名和密码。

### JWT

`JWT` 全名 `json web token`，它是一种开放的标准，其带有数字签名，用于 `json` 对象的安全传输。

# 怎么生成 token

我们已经知道 `token` 是一串字符，我们可以通过一些秘钥+用户名+时间戳等字符组合，使用 `base64` 对其进行加密，从而生成 `token` 颁发给客户端。然后对客户端携带的 `token` 进行解密，拿到秘钥，用户名，时间戳，最后对这些参数进行校验就可以判断 `token` 正确与否和是否过期。

> 以上为 `token` 生成的原理，在实际开发中，我们可以直接使用现成的第三方库（如：`python-jose`）。

### 常用的 JWT 库

- `python-jose`
- `pyjwt`
- `jwcrypto`
- `authlib`

### 安装 JWT 库

```
pip install python-jose
```

### 生成 token

```python
# 从jose导入jwt，后面使用jwt生成token
from jose import jwt

# 导入日期模块，用来验证token过期时间
from datetime import datetime,timedelta

# 定义秘钥，很重要，请勿泄露
SECRET_KEY = 'phyger'

# 生成token的代码，token过期时长定义为默认参数，单位为秒
def create_token(seconds=60):

    # 定义token过期时间，为当前utc时间加上token有效期
    expire = datetime.utcnow()+timedelta(seconds=seconds)

    # 此处即为生成token的payload，sub自定义（可选用户名），uid自定义（可选设备id等）
    # to_endoe可以是一个空的字典，但是不建议这样做
    to_encode = {"exp":expire,"sub":SECRET_KEY,"uid":"123456"}

    # 使用jwt生成token，token是根据payload和秘钥共同生成。
    jwt_token = jwt.encode(claims=to_encode,key=SECRET_KEY)

    return jwt_token
```

> `jose` 的 `JWT` 默认采用 `HS256` 加密方式。

**运行代码**

```
> python utm.py
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTI1MjY0OTgsInN1YiI6InBoeWdlciIsInVpZCI6IjEyMzQ1NiJ9.TnRFBFX_2Jn3VU26n603l5uOQyB9bOOWSxBQUr6tBA4
```

可以看到，`token` 已经生成。

---


> 上面，我们已经介绍了 `token` 的生成，是直接使用的第三方库 `jose`，当然 `jose` 可以生成 `token`，想必他也可以校验 `token` 了。

# token 校验

### 代码

```python
from jose import jwt
# 导入token校验的两种异常，一种是token超时异常，一种是token错误异常
from jose.exceptions import ExpiredSignatureError, JWTError
def judge_token(token):
    # 尝试解密，解密成功后，秘钥，payload，有效时长校验通过，则会返回payload
    try:
        payload = jwt.decode(token,SECRET_KEY)
        print(payload)
        return True

    # 否则，则捕获异常，进行提示
    except ExpiredSignatureError as e:
        print('token过期了！')
        return False
    except JWTError as e:
        print('token验证失败！')
        return False
```

> 按照传统的 `jwt` 协议，我们需要解密 `token` 后，对 `token` 的秘钥，`payload`，有效时长进行单独的校验。以上，`token` 的秘钥，`payload`，有效时长，`jose` 都帮我们完成了，我们只需要调用 `jose.jwt` 的 `encode` 和 `deode` 就可以完成加解密。

### 执行校验

```python
if __name__ == "__main__":
    tk=create_token()
    print(tk)
    res1=judge_token(tk)
    print(res1)
    import time
    time.sleep(60)
    res2=judge_token(tk)
    print(res2)
```

**执行结果**

````python
> python utm.py
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTI1Mjg0MzYsInN1YiI6InBoeWdlciIsInVpZCI6IjEyMzQ1NiJ9.yVhoAKyZFvQi3q4wqd1JoRondl9A6wUaALueP00oyhc
{'exp': 1612528436, 'sub': 'phyger', 'uid': '123456'}
True
token过期了！
False```

> 因为默认token的有效期为60秒，我们在第二次校验token前睡眠了61秒，所以第二次的校验结果为过期！

**使用错误的token校验**
```python
if __name__ == "__main__":
    res=judge_token('phyger666')
    print(res)
````

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6e27019786254693a024c34fe63b3e67~tplv-k3u1fbpfcp-zoom-1.image)

> 以上就是本篇的全部内容了，感谢您的阅读，我们再会。

