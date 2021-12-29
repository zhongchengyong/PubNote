# O3CPU实现分析
Gem5 O3 CPU参照Alpha21264微架构实现了一个乱序CPU模型，基于这一模型可以进行微架构的研究。
## 流水线
* Fetch
在每个cycle都进行取指，在这一阶段创建DynInst对象，分支预测也在该阶段进行处理。
* 译码
> handles early resolution of PC-relative unconditional branches

* Rename
基于物理寄存器list进行指令重命名；如果寄存器资源不够则stall流水线。

* Issue/Execute/WriteBack
Gem5在IEW stage实现指令的Dispatch、Issue、Execute和WriteBack功能，在execute()函数调用时，execute和writeback操作都将执行。

* Commit
指令提交，并在当前stage处理之前可能产生的任何异常。在分支预测错误时，处理前端重定向。

## ISA Independence
O3CPU实现时，将pipeline、resource和lower level CPU代码部分的代码实现为指令无关。ISA相关的代码实现ISA相关的逻辑：
> The lower level CPU, the FullO3CPU, handles orchestrating all of the pipeline stages and handling other ISA-independent actions. We hope this separation makes it easier to implement future ISAs, as hopefully only the high level classes will have to be redefined.

但是在最新的gem5中，已经将架构相关的实现放到了src/arch/<arch>目录下，O3CPU的运行仅依赖O3CPUImpl特化FullO3CPU。

## 代码实现
### 计算类指令

### Load/Store指令

### 分支预测错误

### 数据相关性检查

## Fetch调用堆栈和关键信息

在Fetch时已经调用了Decoder::Decode进行译码，其中Decoder是ISA-dependent的RiscvISA，在这一步骤中得到StaticInstPtr，并使用该StaticInstr构建DynamicInstr对象。

![image-20211219180134938](/home/zhong/.config/Typora/typora-user-images/image-20211219180134938.png)
