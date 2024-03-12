# pick-ticket-damai

大麦捡漏/aiohttp  **仅供参考，学习**

# 2023年10月修复可用.12月大麦更新,本项目失效.
修复总结:
参考Android逆向APK抢票接口加密参数分析文章
环境wireshark frida jadx-gui
通过rpc调用提供python编程接口得到加密参数进行调用

### 环境

- Python >= 3.7 (最好低于3.10)

- 依赖模块安装：```pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/```
- 运行：python run.py 

### 使用
- cookie：[详见](https://github.com/lktlktlkt/ticket-damai/issues/15);
     cookie.py中实现了获取方法

- 主要配置：自用建议使用yaml进行配置

    ```python
    COOKIE = None   # 必填
  
    ITEM_ID = None  # 演唱会url中id或itemId
    CONCERT = 1   # 场次 格式 1 或者 [1, 2]
    PRICE = 1    # 价格 格式 1 或者 [1, 2], 依次对应票档。目前只有`SalableQuantity`类支持list，否则值为下标0
    TICKET = 1   # 购票数量
    
    RUN_DATE = None   # 自定义抢票时间。为兼容优先购，有特权或者演出无优先购可不配置，格式：20230619122100
    DELAY = 0   # 延迟，1=1s。大于0会在RUN_DATE加对应的时间
    
    """System"""
    # 可继承`ApiFetchPerform`，自定购票逻辑，在example.example3中有扩展
    PERFORM = 'damai.performer.ApiFetchPerform'
    ```

- 在代码中主要关注performer，example3。类中有使用注释。

### ps
- 提前登录, 提前在大麦app中添加观演人及收货地址电话。
