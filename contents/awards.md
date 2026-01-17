**隐私保护-静态信息流跟踪与控制**



组成：Android移动客户端，Java云端服务器（集成改进版FlowDroid静态分析模块与SOOT插桩框架），FSAFlow演示系统。



目的： 旨在解决传统静态分析缺乏运行时信息以及动态分析开销过大的问题。通过结合静态预分析与动态路径跟踪的混合分析（Hybrid Analysis）方法，利用状态缩减策略（State-Reduction Strategy），实现对Android应用中隐私数据从源头（Source）到接收点（Sink）的低开销、高精度的动态路径监控与拦截控制。



操作流程：
① 用户首先在移动客户端上为目标应用程序定制隐私流向策略（Flow Policy），随后通过WebSocket协议将该策略文件连同对应的APK文件上传至云端服务器。
② 云端服务器接收到文件后进行静态分析，利用改进的IFDS算法框架挖掘所有违反策略的潜在隐私泄露路径，并记录路径中的关键分支节点信息。
③ 服务器根据分析结果进行静态插桩，仅在潜在泄露路径的起始、结束及关键分支处插入轻量级监控代码，随后将应用重打包并返回给客户端，将其转化为具备策略执行能力的安全应用。
④ 用户在移动端运行经安全增强的应用，系统基于下推自动机（Pushdown Automaton）在运行时高效监控路径状态的变化（包括智能处理循环结构的传播与稳定期），一旦检测到完整的隐私泄露路径形成，即动态阻止信息的泄露。

<div class="ratio ratio-16x9 my-3">
  <video controls playsinline preload="metadata">
    <source src="static/assets/video/static-control.mp4" type="video/mp4" />
    你的浏览器不支持 MP4 视频播放。
  </video>
</div>

