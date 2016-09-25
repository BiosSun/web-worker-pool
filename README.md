# Worker Pool

一个简单的线程池模块，用于统一的维护多个线程。

## 安装

```shell
$ npm install web-worker-pool
```

## 示例

```javascript
// 导入线程池模块
import WorkerPool from 'web-worker-pool';

// 创建线程池
var pool = new WorkerPool('./worker.js');

// 注册任务
pool.register(function(workerAgent) {
    // 监听 worker 传过来的消息
    workerAgent.onmessage = function() {
        // 消息处理代码...
    }
    
    // 监听 worker 中抛出的异常
    workerAgent.onerror = function() {
        // 异常处理代码...
    }
    
    // 或者通过注册消息事件的方式获取消息
    workerAgent.addEventListener('message', function() {
        // 消息处理代码...
    }, false);
    
    // 通过 postMessage 方法发送消息
    workerAgent.postMessage('message content...');
    
    // 当 worker 使用完后，调用 release 方法释放 worker。
    workerAgent.release();
});
```
