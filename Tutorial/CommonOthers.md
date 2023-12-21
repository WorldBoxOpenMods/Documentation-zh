# HarmonyPatch

当你想要修改游戏本身的一些函数, 或者在游戏的函数执行前后进行一些操作, 你就需要用到这个`HarmonyPatch`

入门参考[传送门](https://space.bilibili.com/1306433/article), 专栏里自己找, 可以直接跳转`Harmony补丁基础`部分.

文档参考[传送门](https://harmony.pardeike.net/articles/intro.html)

`HarmonyPrefix`来覆盖整个目标函数提供了极大的自由度, 自然是非常简单的, 但非常容易造成与其他模组的兼容问题. 特别是对于一些"热门"的函数.

所以这里推荐两个可以缓解兼容问题的方式

## HarmonyTranspiler

通过修改游戏函数的IL代码来插入你想要的功能, 具有一定的学习成本, 但相当灵活, 并且具有比`HarmonyPrefix`等高得多的运行效率.

## Listener-Handler

这是NML引入的一个功能, 简单来说, NML或其他模组提供使用`HarmonyTranspiler`实现的`Listener`来监听原版的函数执行, 并依次调用`Listener`下注册的所有`Handler`来处理.

NML还会捕获`Handler`执行时发生的异常, 当异常数量大于一定值后, 将会停用该`Handler`来保证游戏的正常运行.