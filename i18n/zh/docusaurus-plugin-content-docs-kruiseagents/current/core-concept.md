# 核心概念

## Sandbox
Sandbox 是 OpenKruise Agents 的核心 CRD。它负责管理沙箱实例的生命周期，并提供包括暂停（Pause）、恢复（Resume）、检查点（Checkpoint）、克隆（Clone）以及原地升级在内的高级功能。

## SandboxSet
SandboxSet 是用于管理 Sandbox 的工作负载。其功能类似于管理 Pod 的 ReplicaSet。它通过预热沙箱实例池，实现了沙箱的亚秒级启动。SandboxSet 专为扩缩容性能进行了优化，能够在沙箱被消耗时快速进行补充。


## SandboxClaim
SandboxClaim 是从 SandboxSet 中申请（Claim）一个未使用 Sandbox 的请求。一旦某个 Sandbox 被申请，它将不再对其他申请请求可用，并将经历一系列后处理流程，包括原地更新和动态存储挂载。

## SandboxTemplate
SandboxTemplate 是一种不可变资源，代表沙箱模板的一个修订版本。如果 SandboxSet 的模板正在发生变更，它可能会包含多个 SandboxTemplate。

## Checkpoint
Checkpoint 是沙箱中间状态（可能包括内存、根文件系统等）的快照。检查点可以从正在运行的 Sandbox 中创建，并可用于克隆多个沙箱。检查点与创建它的 Sandbox 所属的 SandboxTemplate 相关联。


