#### 编写合约常见问题

##### 合约写日志

- 在合约代码中
```solidity
contract SimpleDemo {
    int256 storedData;
    event AddMsg(address indexed sender, bytes32 msg);
    ...

    function setData(int256 x) public{
        storedData = x;
        AddMsg(msg.sender, "[in the set method]");
    }
    ...
}

```

- 在脚本中

```javascript
    var event = instance.AddMsg({}, function(error, result) {
        if (!error) {
            var msg = "AddMsg: " + utils.hex2a(result.args.msg) + " from "
            console.log(msg);
            return;
        } else {
            console.log('it error')
        }
    });

    function hex2a(hex) {
    var str = '';
    for (var i = 0; i < hex.length; i += 2) {
        var v = parseInt(hex.substr(i, 2), 16);
        if (v) str += String.fromCharCode(v);
    }
    return str;
}
```

##### 调用合约注意事项

- 合约调用合约，不能使用不定长字符串作为阐述
```
 string 是不可以，bytes32 可以
```