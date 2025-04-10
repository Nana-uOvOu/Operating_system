# 第一章 概论
1. 单CPU；多任务；CPU能和外设并行操作。
## 什么是操作系统
1. OS定义：是配置在计算机硬件上的第一层软件，是对硬件系统的首次扩充.OS是**直接控制和管理计算机硬件、软件资源，合理地对各类作业进行调度**，以方便用户使用的程序集合；完成硬件相关，应用无关的操作。
2. 引入OS的目标：
   1. 有效性：合理分配软硬件资源，组织工作流程
   2. 方便性：提供用户对硬件的接口
   3. 可扩充性：系统互操作，硬件拓展
## 操作系统历史
1. 无操作系统阶段：
   1. 串行，用户人工操作，用户独占全机
   2. 利用率 = 执行时间/(执行 + 读卡时间)
2. 单道批处理系统:
   1. 使用系统提供的作业处理语言JCL将所有作业输入，之后用户不在干预，*提高了利用率*
   2. 一个作业包括：用户程序、数据和作业说明书（作业控制语言）
   3. **批**：一个包含多个作业的，供一次加载的磁带或磁盘，使用一组相同的系统软件
   4. 自动性，顺序性，单道性
3. 多道批处理系统：
   1. 通过作业调度算法，将用户作业放入*后备队列中*，使得作业共享CPU资源（IO和CPU共同工作）。
   2. 宏观上并行，利用率高，但用户交互性差。微观上串行，各任务交替使用CPU。
## 操作系统基本类型
批处理操作系统、分时操作系统、实时操作系统。同时拥有两个以上的称为*通用操作系统*
1. 分时：一台计算机的一个周期分给多个用户使用。
   1.  时间片：将系统资源（尤其CPU时间）在时间上进行分割，每个时间段称为*时间片*，每个用户轮询使用时间片
   2.  分时技术：将处理机时间分成时间片，分配给各联机作业使用
   3.  分时操作系统：是一种联机的*多用户交互式的操作系统*。对每个用户能保证足够快的响应时间，并提供*交互会话能力*。**主要用于交互式作业而不是批处理作业**
   4.  特征：交互性（用户和系统人机对话），多路性（多用户用一个机器），独立性（每个用户独立），及时性（用户能在短时间内获得响应）
2. 实时系统：
   1. *在规定的时间内*完成事件处理。
   2. 分类：
      > 实时控制系统:计算机控制系统，以计算机为核心控制生产过程
      > 实时信息处理系统:响应远程用户的提问，对信息进行检索等.
   3. 实时任务分类：周期性/非周期性
3. ![alt text](image.png)
4. 其他分类：
   1. 多处理机操作系统
      > 紧密耦合,松散耦合
      > 非对称式多重处理,对称式多重处理
   2. 网络操作系统：还能提供网络通信+网络服务。低耦合，以“协议”连接
   3. 分布式操作系统:分散处理和控制，以计算机网络为基础的；高耦合，统一的os
   4. 个人计算机操作系统：
      > 单用户单任务：只允许一个用户上机，且只允许用户程序作为一个任务运行
      > 单用户多任务:只允许一个用户上机，但允许将一个用户程序分为若干个任务并发执行。
## 操作系统基本特征
最基本特征：并发、共享，两者相互存在关联。只有并发才能共享。
1. 并发：多个任务在同一*时间段*发生，操作系统要管理这些并发；并行：同一*时刻*发生。
2. 共享：多个进程**共享有限的计算机系统资源**。操作系统要对系统资源进行合理分配和使用。资源在一个时间段内交替被多个进程所用。
   1. 互斥共享：资源分配后不能被其他进程使用。如打印机
   2. 同时访问，如磁盘文件。
3. 虚拟：一个物理实体（CPU，磁盘）分成多个虚拟逻辑实体（分时，分空间）
4. 异步性：不确定性，进程执行顺序和时间不确定（由于分时等操作）
## 操作系统功能
操作系统组成：
1. 管理模块：针对不同管理对象的程序模块（核心kernel）
2. 用户接口：如外壳(shell)、窗口系统。在shell中，通过运行其他程序来完成各种功能
##### 处理机管理
进行*处理机资源调度*等问题。
1. *进程控制*：进程创建，撤销，挂起等。
2. *进程同步*：同步进程之间的*推进步骤*，分配处理机资源，确保*并发*的作业进程资源共享（互斥，同步方式）
3. *进程通信*：进程之间的数据交互。（读取进程，处理进程，打印进程）
4. *进程调度*：
   1. 作业调度：从作业的*后备队列*中选取若干个创建进程
   2. 进程调度：从进程的*就绪队列*中选取一个执行。
##### 存储管理
目标：提高利用率、方便用户使用、提供足够的存储空间、方便进程并发运行
1. *存储分配与回收*
2. *存储保护*：保证进程间互不干扰、相互保密；
3. *地址映射*：进程逻辑地址到内存物理地址的映射；
4. *内存扩充*：提高内存利用率、扩大进程的内存空间。
##### 设备管理
目标：方便设备使用、提高CPU与I/O设备利用率
1. *设备操作*：通过驱动程序完成对设备的操作。
2. *设备独立性*：提供统一的I/O设备接口，使应用程序独立于物理设备，在同样的接口和操作下完成不同的内容
3. *设备分配与回收*：在多用户间共享I/O设备资源。
##### 文件管理
解决软件资源的存储、共享、保密和保护
1. *文件存储空间管理*：为文件分配外存空间，提高外存效率
2. *目录管理*：解决文件检索问题
3. *文件的读写管理和存取控制*：根据用户需求从外存中存取数据。还要求文件保护，防止没有权限的用户读取。
4. 软件管理：版本管理，依赖管理等
##### 用户接口
*提供一个访问操作系统的友好接口*。一般有命令或系统调用。
1. *命令接口*：
   1. 联机用户接口.为联机用户提供,由键盘操作命令及命令解释程序所组成
   2. 脱机用户接口（批处理用户接口），为批处理作业的用户提供.由JCL组成
2. *程序接口*：用户程序获取系统资源服务的接口，由一组系统调用组成
3. *图形接口*：用户鼠标操作
## OS系统设计
1. 无结构操作系统：由众多过程构成
2. 模块化操作系统结构：模块化程序设计，将OS划分为多个小模块，小模块又分为更多模块。但划分根据功能，*没有区别对待共享资源和独占资源*。所有模块都处于内核中，一个崩溃则整个os都会崩溃3. 分层式操作系统结构：OS划分为多层，*每一层只能调用低层服务*。
4. 微内核的OS结构：OS内核只实现基本功能，*其他服务由用户态的进程实现*，C/S模式。用户程序（Client）通过OS内核向OS进程（Server）发送请求来获取系统服务。频繁切换内核态，系统并不高效。
## 双模式操作
1. 内核程序是操作系统最重要的程序。操作系统有内核Kernel就够了，但操作系统不只有内核（还有可视化界面等）。
2. 只有Kernel可以执行特权指令（内存清空等）。所以**CPU状态**分为：
   1. 内核态：管态，内核态，特权模式
   2. 用户态：目态，用户模式
3. 在PSW程序状态字寄存器中存在一位用于表示管态和目态。
4. 管态和目态切换方式：
   1. 管--目：一条特权指令，设置PSW对应位为用户态（目态），*表示操作系统主动让出控制权*
   2. 目--管：*由中断引发，只有当需要操作系统处理时，操作系统才强制夺回CPU控制权*；或当用户程序需要调用系统服务时切换。
5. 双模式操作目的：可以确保系统和用户程序不受错误的用户程序的影响.
6. 进行I/O保护：*所有I/O指令都是特权指令*
7. 存储保护：*防止进程访问其他进程内存，必须通过系统调用才能访问OS核心区*；增设**基地址寄存器，界限寄存器**，用以记录进程基地址和使用内存大小。
   1. 核心态（管态）可以访问任何内存（Kernel和用户进程空间）
   2. 设置基地址，界限寄存器的指令是特权指令。
8. CPU保护：存在硬件设置*时钟*，每个用户进程每N毫秒（时间片）中断一次，将CPU还给操作系统，*是实现分时系统的基础*；修改时钟指令是特权指令。

## 做题
1. 单处理机系统中，进程之间不能*直接并行*，而是*宏观并行*，微观串行。处理机和通道、设备之间都是并行的
2. 提高单机资源利用率的技术是：*多道程序设计技术*
3. 多道程序设计技术中，前提条件是能够实现并发，使用进程调度来提高效率，**前提技术是中断技术**。同时，借助中断技术，可以实现某个进程等待IO工作时先执行其他进程，**实现了CPU与IO设备并行**。
4. 操作系统必须提供**中断处理程序**，不一定非要提供系统调用。
5. 系统调用指令**的执行**必须在内核态，*而发生系统调用可能出现在用户态*。
6. 内部中断：CPU内部引起的（异常），如缺页中断，访管trap指令等；外部中断：CPU外部引起，如时钟中断。
7. 系统调用需要保存PSW，而一般调用不需要保存PSW。
8. 外部中断处理过程中，PC、PSW值由硬件保存，然后硬件将状态切换为内核态，*操作系统需要保存通用寄存器*
9. 分层式设计*更加便于调试*
# 第二章 进程的描述与控制
进程：一个具有一定独立功能的程序在一个数据集合上的一次动态执行过程。*是处理机，存储器和外设的最基本单位*
## 程序的执行特征
1. 顺序执行：**单道批处理/程序设计**。有顺序性（顺序执行）、封闭性（独占全部资源）、可再现性（初始条件相同则结果相同）。
2. 并发执行：**多道程序设计***如果不进行额外处理*，则有间断性（运行中可能中断）、非封闭（共享资源，可能被其他进程修改不变特征）、不可再现。所以必须要**额外操作来保证封闭性和可再现性**
## 进程的定义和特征
1. 进程中包含：
   1. 程序代码
   2. 程序数据、堆（程序员分配，malloc、new等，以链表形式存储）、栈（系统自动分配）
   3. PC等寄存器值
   4. 一组系统资源
2. 进程和程序：
   1. 程序是进程基础，进程是程序功能体现
   2. 程序是*静态*的，进程是*动态*的
   3. **通过多次执行，程序可以产生多个进程；通过调用关系，进程可以调用多个程序**
3. 进程特征：
   1. 动态性：创建产生，调度执行，撤销消亡。拥有*动态地址空间*。
   2. 并发性：内存中有多个进程，宏观上同时执行
   3. 独立性：除非相互通信，否则内存相互独立，*是资源调度的基础*
   4. 异步性：每个进程按照独立的速度进行
   5. 结构性：进程控制块(PCB，位于核心区) +  程序 +  数据 =  进程实体
## 进程控制块PCB
进程控制块（PCB，Process Control Block）是描述进程的数据结构，*记录用于描述进
程执行情况及控制进程运行的全部信息*。
1. 进程组成：
   1. PCB：操作系统为每个进程都维护一个PCB，保存进程的动态特征。
   2. 代码块：描述进程功能
   3. 数据块：描述操作对象和工作区
2. **PCB是进程存在的唯一标识**
3. PCB位于*核心区*，只能通过系统调用间接访问
4. PCB有什么：
   1. **进程描述信息**：进程标识符（内部标识符）；进程名（外部标识符）；父进程标识；用户标识符
   2. **处理机状态信息**：保存运行现场（PC，通用寄存器，PSW，栈指针）
   3. **进程调度信息**：用于操作系统调度；包括进程当前状态，优先级，运行统计信息等
   4. **进程控制信息**：程序段和数据段的地址；进程间同步和通信；资源占用信息（剩余资源）；链表存储的下一个进程指针。
## 进程基本状态
![alt text](image-1.png)
## 进程调度队列
操作系统维护很多队列，*用于表示进程状态*，如就绪队列，各种阻塞队列等；每当PCB记录的状态改变时，会脱离原先队列而加入正确队列。
1. PCB组织方式
   1. 链表
   2. 索引表：同一个状态的PCB装入同一个index表，一个index指向一个PCB。
2. PCB进程切换:![alt text](image-2.png)
## 进程控制
*进程管理中的最基本功能*
1. 进程生命周期：创建、运行、等待、唤醒、终止
2. 进程控制任务：进程的*创建、终止、进程状态的转变*等
3. 进程控制*由OS内核的原语*完成。
> 原语：由若干条指令构成的“原子操作(atomic operation)” 过程；
> 许多系统调用是原语，但原语不一定是系统调用。

4. 内核Kernel功能：*支撑功能；资源管理功能*
##### 进程创建
1. 父子进程：PCB中包含家族关系表项；子进程可以继承父进程资源，撤销子进程需要归还继承的资源；撤销父进程必须同时撤销子进程。
2. 进程创建定义：发生创建新进程事件后，*调用进程创建原语Creat()创建新进程*
3. 引起进程创建的事件：
   1. 系统初始化（系统内核创建）：分时系统的用户登录；批处理系统的作业调度。
   2. 提供服务（系统内核创建）：*用户请求创建进程*
   3. 应用请求（应用自己创建）：应用调用了原语Creat()
4. CREAT()原语：
   1. 申请空白PCB.
   2. 新进程分配空间.
   3. 初始化PCB：标识符；设置PC、SP；进程状态、优先级
   4. 插入就绪队列
##### 进程终止
1. 终止分类
   1. 正常结束：exit
   2. 异常结束：越界错误、超时错误等
   3. 外部干预：系统kill，（被）父进程终止
2. 终止过程
   1. *查询进程状态*：PCB表中检索出对应PCB，查询对应状态。
   2. *终止执行进程*：若处于执行状态则终止，设置调度标志为真并重新调度。
   3. *终止子进程*
   4. *释放资源*：将资源还给父进程，释放内存和lock
   5. *移除PCB*：将PCB从队列中移除
##### 进程的阻塞
1. 引起阻塞的条件
   1. 请求系统服务
   2. 启动操作
   3. 新数据尚未到
   4. 无新工作可做
2. 阻塞过程
   1. 若正在运行态，则调用阻塞原语BLOCK()，进入阻塞态。（是进程的主动操作）
   2. 引起处理机调度
3. Block()
   1. 保存当前CPU现场
   2. 置PCB阻塞态
   3. 进入等待队列
   4. 引起调度
##### 进程唤醒
1. 唤醒原因：等待的事件到达
2. 当其他进程发送信号到唤醒进程后，设置PCB状态为就绪。
3. WAKEUP()原语：
   1. 从等待队列中摘下被唤醒进程
   2. 置为就绪态
   3. 进入就绪队列
   4. 进程调度
4. Block()和WAKEUP()是功能相反的原语，*一个进程Block后一定要Wakeup*
5. ![SB](image-3.png)
##### 进程挂起
1. 挂起原因：
   1. *终端用户请求*：用户发现进程有问题，请求暂停
   2. *父进程请求*
   3. *负荷调节需要*：资源紧张时，将低优先级进程等暂时不执行的进程挂起，腾出空间
   4. *操作系统的需要*：检查资源或记账使用
2. 挂起作用：合理且充分地利用系统资源；进程挂起时，不在内存中，*仅在磁盘上存在镜像*
3. 挂起原语：SUSPEND():
   1. 将进程从内存调到外存，修改状态（PCB不修改）
   2. 若处于活动就绪/活动阻塞状态，则修改为静止就绪/静止阻塞
   3. 若运行，则重新调度
4. 激活原语：active():
   1. 原因：父进程或用户进程请求，或内存已有足够空间
   2. 从外存调入内存，改变进程的状态
5. ![alt text](image-4.png)
## 进程同步
进程具有**异步性**的特征。
*异步性*：各并发执行的进程以各自独立的、不可预知的速度向前推进。必须要通过某种机制同步起来
1. 进程之间的制约关系：
   1. 间接制约：两进程之间*资源共享*导致的制约
   2. 直接制约：进程间相互合作导致的制约
2. 临界资源：一个时间段内只允许一个进程使用的资源称为临界资源
##### 有限缓冲区的生产者与消费者问题
**生产者进程生产的信息由消费者进程消费**
假设生产者和消费者对于缓冲区有一个变量counter用于记录缓冲区数据数量。
1. 问题所在：
   1. 生产者生产数据后需要counter++;消费者消费数据后需要counter--
   2. 对应汇编代码：
   ```
   // 生产者
   LOAD Reg1 counter
   inc Reg1
   Store counter Reg1

   // 消费者
   LOAD Reg2 counter
   dec Reg2
   Store counter Reg2
   ```
   3. 当并发处理时，生产者和消费者汇编代码可能出现问题
   ![alt text](image-5.png)
2. *进程并发地共享数据导致不一致性*。需要保证counter++和counter--都是原子操作：**全过程无间断一次完成**
##### 互斥方式实现对临界资源的共享
1. 临界资源：硬件或软件（如外设、共享代码段），多个进程在对其进行访问时（关键是进行写入或修改），必须互斥地进行。
2. 临界区：
   1. 临界区是进程访问临界资源的一段代码，进入临界区后，*不允许其他进程进入各自的临界区*
   2. 进入区：进入临界区前检查是否可进入的代码。若可进入则设置”正在访问临界区“标志位。
   3. 退出区:清除“正在访问临界区”标志
   4. 剩余区：其他部分代码
3. 处于临界区时，说明这个进程正在使用处理机，*此时可以进行调度*。但存在一些不能调度的情况：
   1. 中断处理
   2. 处于系统内核的临界区时
   3. 处于必须不能中断的原子操作时
##### 同步机制需要满足的
1. 空闲则入：临界区能够进入则进入
2. 忙则等待：临界区满则进入等待
3. 有限等待：不能死等
4. 让权等待：不能进入临界区则让出控制器（转换到阻塞态）
##### 临界区同步算法
1. 2个进程同步：Peterson算法![alt text](image-7.png)
2. n个进程同步：面包店算法：![alt text](image-8.png)
##### 中断屏蔽方法(硬件)
也可以使用中断屏蔽来确保进程的原语性.
1. 过程
    1. 当某个进程访问临界区时,*关中断*,此时不会发生进程切换
    2. 访问临界区结束后,*开中断*,此时可以进行切换
2. 不适用于多处理机,**只适用于系统内核进程,不适用于用户进程**,原因:开关中断指令只能运行在内核态,是特权指令,不能给用户随意使用.
##### TS指令(TestAndSet)(硬件)
1. 也称为Test and set lock指令,*用硬件实现*,执行过程不允许中断.
2. ![alt text](img\(14\).png)
3. 适用硬件实现,简单快捷,适用于多处理机环境.但*不符合让权等待*,会一直忙等,占用CPU进行循环
##### Swap/Exchange/XCHG指令(硬件)
1. 硬件实现,执行过程不允许中断.类似TS指令,先记录原lock值old,再上锁(lock=true),查看old是不是false,如果是false则说明没人访问临界区,可以访问.
![alt text](img\(1\).png)
2. 不符合让权等待.会死等.
## 信号量机制(semaphore) 
##### 信号量设计
信号量是OS提供的管理公有资源的有效手段.
1. 整型信号量:*使用S整型和两个原子操作来标记资源数量,有多余资源则占用一个资源-1,用完退出资源+1*
![alt text](img\(2\).png)
2. 记录型信号量
    1. 一个结构体S,包含`int count`,表示*某种*资源数量;一个`PCB链表 queue`表示阻塞在此信号下的进程的PCB队列.
    2. P原语(Wait):
    ```C
    --s.count;
    if(s.count<0){
        BLOCK(s.queue); // 资源量不够则阻塞请求资源的进程,且放入等待队列中.
    }
    ```
    3. V原语(Signal):
    ```C
    ++s.count;
    if(s.count <=0){
        WAKEUP(s.queue); // 释放时增加资源量,并唤醒等待队列的第一个阻塞进程
    }
    ```
    4. `S.count >= 0`:表示剩余资源量
    5. `S.count < 0 `:小于0时,绝对值表示阻塞的PCB量
    6. `S.count`初值为1时,表示只允许一个进程访问临界资源,*实现互斥* 
    7. **进程共享的资源量越多,越容易造成死锁**
3. AND型信号量
    1. 思想:一次性将需要的资源给到进程,只要有一个资源不够就全都不给
    2. 原子操作同时wait:`Swait()`;同时Signal`SSignal`
    3. 注:Swait中,若对于某个$S_i$不够,则将该进程放入$S_i$的等待队列并阻塞,然后回到Swait起点.
    ![alt text](img\(3\).png)
4. 二进制信号量
    1. 二进制信号量`bin S1=1,bin S2=0,int C=共享资源初值`
    2. 可用于实现整型信号量
5. 信号量集
    1. 为了一次获取多个资源,拓展AND型信号量:`S`信号,`t`下限值,`d`需求量
    2. ![alt text](img\(4\).png)
    3. 信号量集的使用例:
        > 1.Swait(S,d,d):一次分配d个资源,资源量少于d不予分配
        > 2.Swait(S,1,1):退化为记录型信号量(S>1);互斥信号量(S=1)
        > 3.Swait(S,1,0):可控开关,当`S>=1`则可以进入多个进程,`S=0`就都不能进.
##### 信号量应用
1. *实现临界资源的互斥访问*
设置一个互斥信号量`mutex=1`,并将原语`Wait(mutex)`和`Signal(mutex)`放在临界区上下.
```C
semaphore mutex = 1;   
do{
    …
    wait ( mutex );
    critical section
    signal( mutex );
    remaider section
}while (true);
```
> 注意:`wait`和`Signal`必须成对出现,缺少wait则不能互斥访问临界资源,缺少signal则资源不会被释放.
2. *实现同步操作*:
    1. 前驱关系:并发执行的进程`P1,P2`,要求对应代码`C1`在`C2`之前完成
    2. 设置互斥信号量`S12 = 0`.
    ```C
    C1;
    signal(S12)

    ///
    wait(S12)
    C2;
    ```
    3. 必须等C1结束后S12++,C2才能跳出wait()执行.
3. *同步操作例题*:
    1. ![alt text](img\(5\).png)
    2. ![alt text](img\(6\).png)
## 管程的基本概念
管程是一种*进程同步方法*.
1. 为什么引入管程:当使用信号量同步时,若同步进程过多,信号量分散,导致管理困难,容易死锁.
2. 管程目的:记录资源,所有访问资源的进程必须通过管程,且管程只允许一个进程访问,实现了互斥.*但使用信号量的效率比管程高*.
3. 管程定义:
    1. 对于某个资源,管程定义了一个*数据结构和对这个结构的操作*,可以通过这些操作同步进程,修改数据结构中的数据.每次只允许一个进程进入管程,若多个进程进入,则只有当第一个进程使用完并释放后才能下一个.
    2. 当进程进入管程被阻塞后,只有当前使用管程的进程将管程释放后才能让其他进程使用管程.为了区分等待原因,定义条件变量`condition x,y,...`和两个原语`wait(),signal()`.对于每个原因,若某个进程因此原因被阻塞,则进入对应condition的等待队列.
    3. 当`x`条件不满足时,调用管程的进程会调用`x.wait`,使得调用进程阻塞并进入等待队列;当`x`条件变化后,`x`调用`signal`唤醒队首进程.
## 经典的进程同步问题
##### 生产者消费者问题
一个生产者生产数据,放入*缓冲区*;一个消费者消费数据,从*缓冲区*取出数据;
当缓冲区不满时,生产者才能生成;缓冲区不空时,消费者才能消费;
*缓冲区是临界资源,各进程必须互斥访问*
1. ![alt text](img\(7\).png)
2. ![alt text](img\(8\).png)
3. 注意:必须先进行资源信号量的wait,再进行互斥信号量的wait,否则会死锁.
4. 总结
![alt text](img\(9\).png)
##### 读者,写者问题
1. 问题:![alt text](img\(10\).png)
2. ![alt text](img\(11\).png)
3. ![alt text](img\(12\).png)
4. ![alt text](img\(13\).png)
## 进程通信
每个进程拥有的内存空间是独立的，不能相互直接访问。需要进行进程通信。
1. 进程通信分类
   1. 低级通信：包括状态和简单的整数传递，如信号量和管程机制。*信息量较小，效率低，实现复杂*
   2. **高级通信**：用复杂数据结构传递的大数据量通信，通信效率高。*共享存储器系统、消息传递系统、管道通信系统*。
##### 共享存储器系统
通过增加段表页表的方式，可以将某个内存空间设置为共享空间。
1. 为了避免写冲突，共享空间*互斥*，可以使用操作系统提供的PV操作实现。
2. 共享内存通信的分类：
   1. *共享数据结构*（低级通信）：低效，OS提供共享存储器，用户程序员自己设计数据结构，实现同步通信，*效率低，通信量小*。
   2. *共享存储区*（高级通信）：可以传递大量数据。进程通信前向os*申请一块存储区域*，若不存在则划分，存在则返回区域标识符，并将该进程连接上去。*数据的结构和同步都由进程管理，而不是os*
##### 消息传递系统
程序员直接利用系统提供的一组通信原语进行通信。分为直接通信和间接通信。
1. 直接通信：
   1. 使用os提供的通信指令来通信，以显式方式提供对方标识符：send/receive($P_i$,(&)message)。
   2. 接受进程的PCB内存在消息队列，$P_1$send后将msg放入对应进程$P_2$PCB的消息队列中，$P_2$receive($P_1$,&msg)后将消息队列的信息放入msg中，获得通信的信息。
2. 间接通信：借助os提供的共享数据结构信箱原语进行通信。
   1. 有私人信箱（其他进程只能放入消息），公用信箱（可以通过os核准后发送消息和接受消息）和共享信箱（拥有者批准某些进程访问，每个进程可以取走自己的信息）
   2. ![alt text](image-10.png)
##### 管道通信系统
管道通信系统拥有*一个读进程，一个写进程，一个管道文件pipe*.
1. 写进程可以将大量字符流数据写入pipe，读进程读，*需要互斥，同步，且需要实现判断对方是否存在，存在才可通信*
2. 半双工通信，同一时间只能单向传输。想要同时双向传输需要两个管道。
3. 管道满时写进程阻塞，空时读进程阻塞。
## 线程（Thread）
线程是比进程更小的可独立运行的*基本单位*。引入线程的目的是用它来提高系统内程序的并发程度.提高系统效率，增大系统作业的吞吐量。
1. 线程与进程比较：
   1. 引入线程后，**线程是处理机分配（调度）的最小单元，进程是除CPU外的系统资源分配的最小单元**。
   2. 线程之间可以并发执行，且共享同一个内存空间。
   3. 进程切换时需要切换环境，开销大；线程不用，开销相对较小。、
   4. 线程同样具有*就绪、阻塞和执行*三种基本状态。
2. 线程的属性
   1. 共享进程资源：进程的地址空间，信号量，计时器等
   2. 轻型实体：每个线程只拥有少量资源(标识符，TCB：包含PC和少量寄存器信息，核心栈，局部变量)
   3. *调度最小单位*
   4. 可并发执行
3. 线程优点：
   1. 一个进程多个线程，线程并发执行
   2. 创建和终止时间短
   3. 线程之间共享资源，不用通过系统内核
4. 线程缺点：*一个线程崩溃则整个进程崩溃*
##### 用户级线程
仅存在于用户空间中，无需内核支持，内核不知道线程的存在。**一个线程发起系统调用而阻塞，则整个进程都要等待**。由*线程库*实现，所有线程相关操作都由应用程序完成，在用户态实现，速度快。
1. 当一个时间片被分配给进程，则需要额外分配给多个线程，*每个线程得到的时间少*。
2. TCB在用户空间中。
##### 内核级线程
由OS支持，用户程序和内核程序线程都由内核操作，一个线程阻塞不会导致整个进程被阻塞，*能在多处理机上并行执行*。
1. TCB在内核空间中
2. 线程切换在内核态，切换开销大。
3. 有不同多线程模型：
   1. 多对一模型：多个用户级线程*运行在一个内核线程上*，仍然需要线程库帮助，一个阻塞则全部阻塞，线程切换在用户态进行，不能再多处理机上并行。**重点：操作系统只看得见内核级线程，处理机调度分配的基本单位是内核级线程**
   2. 一对一模型：一个用户级线程阻塞后不影响其他线程，但切换线程需要切换到内核态，且创建线程开销大，*限制了线程总数量*。
   3. 多对多模型：n个用户线程通过*多路复用*分配到$\leq$n个内核级线程上。允许操作系统根据资源配置情况控制创建内核线程的数目。**内核级线程才是处理机调度的基本单位**。
## 做题
1. 单处理机系统中，**每个时刻最多有1个进程处于运行态。**也可能没有运行态：死锁，**此时全都在阻塞态**
2. 线程切换*可能引起进程切换*：从A进程的线程切换到B进程的线程
3. **引入线程可以减少程序的时空开销**
4. 用户级线程**不能再多处理机上并行**，因为操作系统只能看到进程。
5. 线程不共享进程的栈。
6. 临界区是指*访问临界资源的代码段*
7. 管程的Signal和V操作不同。V操作一定会使S=S+1，而Signal只会改变某个条件变量，*若没有被阻塞的进程，是不会被改变的*。
8. 管程执行wait后一定会将进程阻塞，放入阻塞队列；通过signal来唤醒阻塞队列第一个进程。
# 第三章 处理机调度与死锁
## 处理机调度的层次和调度算法的目标
##### 作业和进程
1. 作业：（用户）利用计算机进行一次运行所需工作的集合。要完成一个工作，用户必须先提交一个作业。*一个作业可能由多个程序构成*。现在的PC和服务器基本没有作业概念。
2. 作业和进程差别
   1. 作业是用户向计算机提交的*任务实体*。进程是完成用户任务的*执行实体*，是资源分配的基本单位。
   2. 作业建立完毕后放在*外存*等待处理，进程创建后一直在*内存*运行
   3. 一个作业由至少一个进程组成
   4. 作业多用于批处理系统，进程可以用在几乎任何多道程序处理系统
3. 作业调度和进程调度
   1. 作业调度：系统资源满足后，将作业*放入主存储器中*
   2. 进程调度：使作业进程占据处理机
4. 批处理型作业调度过程可能经历*高级（作业）调度，中级（内存）调度，低级（进程）调度*。
##### 调度基本类型和调度方式
1. 调度概念：**在多道程序环境下，进程数目往往多于处理机数目。要求系统能按某种算法，动态地将处理机分配给就绪队列中的一个进程，使之执行**
2. 高级调度：用户有一个任务（多个作业）要做，将这些作业放入外存，并告诉操作系统要完成它。此时os需要启动多个进程来完成这个工作，然而内存等资源可能不够，不能同时启动这些进程来完成所有作业，此时需要进行作业调度，
   1. 又称作业调度或长期调度。根据某种算法，将外存中处于*后备队列*的某个作业调入主存.
   2. 作业创建时建立PCB，作业结束后才撤销PCB
   3. 无→创建态→就绪态
3. 中级调度（内存调度）：
   1. 为了提高吞吐量，降低负荷，系统会将一些就绪/阻塞态的进程挂起，放入外存。
   2. 当系统资源足够，内存稍有空闲时，*通过某些算法将挂起的就绪进程* **对换** *回内存，放入就绪队列*。
   3. 频率比高级调度高。
   4. 挂起态→就绪态
4. 低级调度（进程调度或短期调度）：会根据某种算法将就绪队列的进程通过dispatcher调度程序分配处理机。
   1. **最基本的调度，频率最高**
   2. 就绪态→执行态
5. 调度方式
   1. 非抢先式调度：一旦将处理机分配给某个进程，除非该进程结束或阻塞（调用原语、出错、等待I/O），否则一直占用处理机。
   2. 抢先式调度：运行暂停某个正在执行的程序，将处理机分配给其他进程。有时间片原则，优先级原则和短作业优先原则。
##### 调度队列模型
1. 仅有进程调度：![alt text](image-12.png)
2. 具有高级（作业）和低级（进程）调度：![alt text](image-13.png)
3. 3级调度模型：![alt text](image-14.png)
##### 选择调度算法的准则：系统准则
1. *CPU利用率*：工作时间/总时间；
2. *系统吞吐量*:*使用尽可能少的时间完成多的工作*。系统吞吐量=总共完成了多少道作业/总共花了多少时间。
3. *各种资源的均衡利用*：系统资源的合理利用。处理机和IO繁忙搭配。
##### 选择调度算法的准则：用户准则
1. *周转时间*:**作业从提交到完成（得到结果）所经历的时间为周转时间**。
   1. 包括了：外存后备队列等待时间，就绪队列和阻塞队列等待时间，CPU执行时间，输出时间
   2. **所有作业的**平均周转时间为*所有作业的周转时间/总a作业数*：$\bar{T} = \frac{1}{n} × \sum_i^n(T_i)$
   3. **某个作业的**带权周转时间为*$\frac{作业周转时间}{CPU实际运行时间}=\frac{作业执行总时间-作业提交时间}{作业执行总时间}$*
   4. 平均带权周转时间
2. *等待时间*：指用户的进程或作业*处在等待处理机的状态*的时间之和。等待时间=等待被CPU服务的时间=作业在外存后备队列等待的时间+建立进程后等待服务的时间；*等待I/O完成也属于被服务，不算等待时间。*
3. *响应时间*：分时系统的重要指标。指*用户输入一个请求开始到系统首次响应的时间*。包括用户输入时间，处理机处理时间，处理结果送到终端显示器的时间。
4. *截止时间*：分时系统的重要指标。开始截止时间（某个任务最迟的开始时间）和完成截止时间（某个任务最迟的结束时间）。
5. 优先权原则：让关键任务得到更好的指标。
## 调度算法
##### 作业调度算法
1. *FCFS(First Come First Serve)算法*：最简单的算法，*适用于作业调度和进程调度*
   1. *按照作业提交或进程变为就绪态的顺序*依次获取CPU，一直占用直到阻塞或结束（非抢占）
   2. 当阻塞态恢复后，重新去就绪队列排队。
   3. *有利于长作业/IO不忙/CPU繁忙作业而不利于短作业/IO繁忙作业*
   4. 公平，*不存在饥饿现象*（某个作业/进程长时间得不到处理）
2. *短作业（进程）优先调度算法(Shortest Job/Process First，SJF/SPF)* 
   1. *预计执行时间短的作业优先获得处理机，但不会抢占当前拥有处理机的进程*
   2. 降低平均周转时间和平均带权周转时间，提高吞吐量。*当所有作业几乎同时到达（同时可执行）时，SJF的平均等待时间，平均周转时间最短*
   3. 对长作业很不利，不能考虑紧急程度，而且难以估算执行时间。
   4. *最短剩余时间优先*（SJF的变形，SRF，Short Remain First）,允许执行时间比当前处理机处理的进程剩余时间更短的进程**抢占**处理机。
   5. 不公平，*可能存在饥饿现象*
3.  *最高响应比优先*（SJF变形，HRRN，Highest Response Ratio Next）：
    1.  *非抢占式*，当处理机空出时，计算响应比最高的进程调度。
    2.  响应比R = (已等待时间 + 预期执行时间) / 预期执行时间，是FCFS和SJF的折衷
    3.  当等待时间全一样时，执行时间越短越调度：SJF；服务时间相同，谁等的多谁调度：FCFS；
    4.  响应比的计算增加系统开销。
    5. 不会饥饿
##### 进程调度算法
1. *时间片轮转法*（Round Robin, RR）：
   1. 主要用于微观（进程）调度。*提高资源利用率*。**是抢断式算法**。
   2. 首先将所有进程按照FCFS排成就绪队列，每次给队首处理机，时钟装置发出时钟中断来通知进程时间片完。中断后将进程放到就绪队列尾，上下文切换将处理机给到新队首。
   3. 就绪队列进程越多，时间片越短。时间片过短时，平均（带权）周转时间变长，切换开销过大，处理机资源大量被用于切换。时间片过长时，退化为FCFS， 进程响应时间变长（例如10个进程等待，1s时间片，则用户输入要等待至少9s才有响应）。
   4. 所以设计时要将时间片时间设定为切换耗时仅占用1%。
2. *优先权调度算法*(Priority Scheduling)：
   1. 可用于作业/进程调度。将优先级最高的作业从后备队列放入主存；给优先级最高的就绪队列进程处理机。
   2. 分为抢占式和非抢占式。*可抢占程度越高，系统实时性越好*。有
   > 1. 完全不抢占：可能会导致某进程死循环长期占用CPU
   > 2. 系统态完全不抢占
   > 3. 内核部分可抢占：在可抢占点进行抢占
   > 4. 完全可抢占或内核完全可抢占
   3. 优先级划分：
   > 1. 静态优先级：创建时获得一个优先级，之后*不变*。系统进程优先数高，资源占用少的优先数高；这样系统开销较小。
   > 2. 动态优先级：创建时获得一个优先级，之后*根据情况改变*。等待时间长就增加优先数，运行久则降低优先数。
   4. 系统进程>用户进程；前台进程>后台进程；I/O型进程>普通进程（IO型进程能够和CPU并行操作）；
3. *多级反馈队列调度算法*(Round Robin with Multiple Feedback)
   1. 结合所有方法的特点。*抢占式算法*
   2. 设置*多个优先级的就绪队列，优先级越高则时间片越短*。当一个新进程创建时，优先进入最高级队列，一个时间片未运行完则降低一级队列，放到队尾，一个时间片未执行完再降低一级...。高优先级队列可以抢占处理机，被强占的进程放到*原队列末尾*。
   3. 照顾短进程：缩短周转时间，增大吞吐量；照顾IO进程：降低响应时间，增加IO设备利用率；不必估算进程执行时间，动态操作。
   4. ![alt text](image-15.png)
## 实时调度
1. 实时调度分类：
   1. *硬实时调度*：有一个最后期限，完不成对系统造成很大损失。
   2. *软实时调度*：有一个最后期限，但超过期限完成也有意义
2. 实时调度前提：
   1. 提供相关信息：就绪时间；开始截止和完成截止时间；消耗的资源；处理时间；优先级
   2. 系统处理能力强；![alt text](image-16.png)若不能完成则加强单处理机性能或增加多处理机。
   3. 抢占式调度：具有*硬实时调度的广泛采用抢占式调度*
   4. 拥有快速切换功能。
3. 非抢占式调度算法（用于非周期类实时任务）分类：
   1. 非抢占式*轮转调度*算法：数秒延迟
   2. 非抢占式*优先调度*算法：相对严格，数百毫秒
   3. ![alt text](image-17.png)
4. 抢占调度算法（用于周期类实时任务）分类：
   1. 基于*时钟中断*的抢占式优先权调度：实时进程来到后不立即抢断，*而是等待时间片完再让出*。几十毫秒-几百毫秒。
   2. *立即抢占*的优先权调度算法：只要不在临界区，就直接抢占。几百微秒-几毫秒。
##### 常用的实时调度算法
1. 最早截止时间优先算法EDF（Earliest Deadline First）：
   1. 维护一个实时进程队列，*按照截止时间（开始/结束）从早到晚排序*，每次调度都将处理机给第一个。
2. 最低松弛度优先LLF（Least Laxity First）算法
   1. 用于抢占调度，计算队列中实时进程的紧急（松弛）程度并排序。
   2. 紧急（松弛）程度 = 必须完成的时刻 - 执行时间 - 当前时刻
   3. ![alt text](image-18.png)
## 死锁概述
1. 什么是死锁：是指多个进程在运行过程中因争夺资源而造成的一种僵局，当进程处于这种状态时，若无外力作用，它们都将无法再向前推进
2. 死锁原因：
   1. 可剥夺和不可剥夺资源：
   > 1. *竞争不可剥夺资源*：某个进程获得不可剥夺资源后，只有当使用完才能给其他进程。当两个进程分别拥有部分需要的不可剥夺资源，且一直请求对方拥有的资源时，两个进程死锁。
   2. *竞争临时性资源*：动态生成和消耗的资源。两进程相互请求对方生产的临时性资源时，而不产出对方需要资源时，死锁。
   3. *信号量的使用不当造成死锁*：当互斥的P操作在实现同步的P操作之前，死锁。
3. 死锁必要条件
   1. ![alt text](image-19.png)
   2. *当死锁时一定会有循环等待（循环等待是必要条件），而循环等待未必死锁（非充分条件）*
## 死锁处理
1. 预防死锁
   1. *破坏互斥条件*：只有对互斥资源进行争夺时才发生死锁。使用某种技术将独占资源转换为共享资源。但难以实现，或互斥必须保持
   2. 破坏“请求保持”条件：必须资源分别在多个进程手里，相互之间请求资源，死锁。可以使用*静态分配*策略，一次请求全部资源，只有当全部空闲才能分配到。资源浪费，利用率低。
   3. 破坏“不可剥夺”条件：获取到的不可剥夺资源必须使用完才释放。频繁释放资源，吞吐率降低。
   > 1. 某个进程已经请求到某些资源，再请求资源不能满足时，*释放所有资源*
   > 2. 根据优先级，当某进程得不到资源时在OS帮助下强行剥夺
   4. 破坏“环路等待”条件：有序资源使用法，将资源分类并排序，每个进程按照资源序号请求资源，不形成环路（*持有小序号资源的进程才能请求大序号资源，而持有大序号资源的进程不能逆向请求小序号资源*）。降低利用率，限制自由编程。
2. 避免死锁：
   1. 安全状态：当所有进程可以找到一个序列(P1,P2,...,Pn)依次执行而不死锁时，称为安全状态。要严格按照安全序列执行。
   2. 银行家算法：当每次收到资源请求时，**先判断本次资源分配是否会导致不安全状态，若是则暂时不同意，让进程变为阻塞态**。
   > ![alt text](image-20.png)
   > ![alt text](image-21.png)
   > ![alt text](image-22.png)
   > ![alt text](image-23.png)
   > ![alt text](image-24.png)
   > ![alt text](image-25.png)
3. 死锁的检测：发生死锁时，OS需要检测出是否发生死锁
   1. 定义一个数据结构：![alt text](image-26.png)
   2. 设计一个算法来检测死锁：对于请求边，尝试将请求满足，然后消除边（请求边）；若能够完成某个进程，则会将资源还掉，消除分配边，增加小球数量，然后又可能能够消除其他请求边。**若所有边都可以消除，则不存在死锁，即图是可以完全简化的**（相当于找到一个安全序列）。
   3. 检测算法(类似银行家)：
   ![alt text](image-27.png)
   ![alt text](image-28.png)
   ![alt text](image-29.png)
4. 解救死锁:
   1. *资源剥夺法*：将进程*直接挂起*，并剥夺资源给其他进程。选择进程时，要考虑代价最小，且不能总是让某个进程当牺牲品。注意不能让被挂起的进程长期得不到资源而饥饿。
   > 回滚(Roll-back)：*退回到安全状态并重启进程*；或者直接完全回滚，终止进程并重开。
   2. *撤销进程法*：直接终止部分或全部死锁进程。如何决定撤销？查看进程的优先级、已经消耗的资源数、运行时间等。
   3. *进程回退法*：将一个或多个死锁进程回退到安全状态。要求有历史记录。
## 死锁例题
![alt text](image-30.png)
<<<<<<< HEAD

## 做题
1. 实时系统一般需要处理紧急事务，所以使用*抢占式优先级调度*
2. **绝对可抢占的算法：时间片轮转**，时间到必然被抢走
3. 当进程请求不到资源且有因为该资源而阻塞的进程时，*阻塞进程释放资源*可以避免死锁，但会导致**饥饿**。
4. 当资源分配图中：
   1. **没有环路**：破坏了循环等待，*一定不死锁*
5.  死锁定理用于检测死锁。
6. 银行家算法保证了**每个时刻都有至少一个安全序列，即每个时刻都至少有1个进程能获得所有需要的资源**
## 做题
1. 实时系统一般需要处理紧急事务，所以使用*抢占式优先级调度*
2. **绝对可抢占的算法：时间片轮转**，时间到必然被抢走
3. 当进程请求不到资源且有因为该资源而阻塞的进程时，*阻塞进程释放资源*可以避免死锁，但会导致**饥饿**。
4. 当资源分配图中：
   1. **没有环路**：破坏了循环等待，*一定不死锁*
5.  死锁定理用于检测死锁。
6. 银行家算法保证了**每个时刻都有至少一个安全序列，即每个时刻都至少有1个进程能获得所有需要的资源**

# 第4章 存储器管理
1. 存储器管理的功能：
   1. *存储分配和回收*：主要内容。讨论存储分配算法和数据结构。
   2. *地址变换*：可执行文件的链接技术、程序加载重定位、运行时地址变换等。
   3. *存储共享和保护*：数据共享和保护
   4. *存储器扩充*：存储器逻辑和物理组织
## 地址
1. 物理地址（实地址，绝对地址）空间：*硬件的地址空间*；逻辑地址空间（虚地址，相对地址）：*执行时程序看到的地址空间*。逻辑地址是CPU执行指令时生成的地址。
2. 将逻辑和物理地址分离，是存储器管理的核心。
   1. 程序编译，加载阶段，*逻辑地址和物理地址相同*
   2. 程序执行阶段，*逻辑地址和物理地址不同，使用地址映像机构进行***重定位**
## 程序和指令执行
程序从代码到执行过程为：`编写（代码）→编译（目标模块）→链接（装入模块）→装入（程序）`
1. 程序编译后，机器码所指定的地址是逻辑地址，是*相对于进程起始地址的相对地址*。在程序装载时，程序的起始地址不一定，必须要通过逻辑地址和物理地址的转换映像。
2. 装入模块：代码编译，链接后得到的可执行文件（elf、exe）等，由机器码组成。
3. 程序装入方式：
   1. *绝对装入*：**只适用于单道程序环境**。装入程序按照待装入程序的装入模块*绝对地址*装入。
   2. *静态重定位(可重定位装入)*:装入模块中指令给出的都是相对于程序起始地址0的相对地址。*当装入时，地址映像模块负责重定位，将相对地址转换为绝对地址*。无需硬件支持，可以装入有限多道程序。
   > 当*连续*内存不足以满足程序的全部内存要求时，无法装入；装入后不能再移动。
   ![alt text](image-32.png)
   3. *动态重定位（动态运行时装入）*：装入模块中存放逻辑地址，装入后仍然是逻辑地址，*当执行时动态执行地址转换，需要重定位寄存器（存放存入程序的起始地址）*。可以支持程序执行过程中的地址引用，例如地址指针。
   > 允许在执行时移动；可以分配给不连续的内存地址，给出*比存储空间大得多的地址空间*。
4. 程序编译：将高级语言代码编译为机器语言，得到多个*目标模块*
5. 程序链接：由链接程序将*多个目标模块和库函数*链接在一起，得到一个装入模块。
   1. *静态链接*：装入前将所有目标模块和库函数链接为一个装入模块后，之后不再拆开
   2. *装入时动态链接*：装入时，所有模块*边装入边链接*
   3. *运行时动态链接*：*运行时需要某个目标模块时*，才进行链接。便于修改更新，模块共享。便于局部代码修改，动态链接的dll便于适应运行环境
6. 地址生成：![alt text](image-34.png)
7. 地址安全检查：
   1. 逻辑地址空间由`base`和`limit`寄存器规定，设置这两个寄存器的指令是特权指令。
   2. 用户模式验证地址，发现危险地址则中断进入内核。
## 连续分配存储管理方式
连续分配：为用户程序分配一个连续的内存空间
##### *单一连续分配*
适用于*单用户、单任务的OS*。将内存分为系统和用户两部分，用户程序使用全部用户内存。没有存储保护。
##### *固定分区分配*
1. 分区式存储管理：为了实现多道程序系统，将内存分为相同（相同程序并发执行）或不同（根据程序大小分配）多个分区。os将分区按照大小排队，然后建立一张分区使用表：![alt text](image-35.png)
2. 系统用一个，剩下的用户使用。 
3. *内碎片：占用分区之内未被使用的空间（分区大了）；
4. *外碎片*：分区中难以利用的空闲分区（小分区没人够用）*
##### *动态分区分配*
1. 当程序运行时，os根据进程的实际需要分配内存块（分区）。os持续追踪运行时的已分配内存块和空闲块。
2. 为了管理空闲分区建立了*空闲分区表*或*空闲分区链表*，动态改变，可划分为空闲分区表和占用分区表。
空闲分区表：![alt text](image-36.png)
空闲分区链：![alt text](image-37.png)
占用分区表：![alt text](image-38.png)
3. 分区分配算法：
   1. 当一个进程需要装入，则寻找一个空闲块，大于等于需要大小
   2. 若大于，则将块划分为两个块，一个大小=需要，剩余块空闲
   3. *首次适应算法（first-fit）*：按照分区先后次序，找到第一个适合的空闲块。分配释放速度快，可以将大块留在高地址。然而随着小块增加，*查找时间增加*。
   4. *循环首次适应算法、下次适应法(next-fit)*：设置一个起始查找指针。每次都从上一次查找成功的地址开始找，找到第一个合适空闲块。分配释放速度块，不易保留大块。
   5. *最佳适应法(best-fit)*：从小到大排序空闲块，*找到和需求差距最小的空闲块*。外碎片小而多，大空闲分区可以保留。
   6. *最坏适应法(worst-fit)*：从大到小排序空闲块，*每次分配最大空闲块*。基本不留小空闲分区，但不保留大空闲分区。
   7. *快速适应算法(分类搜索法)*：将分区按照大小分类，同类分区大小相同，建立多个空闲分区链表；系统中建立管理索引表，记录多类分区表头。查询空闲分区效率高，释放慢。

4. 分区分配操作：
   1. 分配内存
   2. 回收内存：
   ![alt text](image-39.png)
   ![alt text](image-40.png)
   ![alt text](image-41.png)
##### 伙伴系统
动态分区方式和固定分区方式的折中。
1. 所有分区大小都固定为$2^k$，其中$1\leq k \leq m$。$2^m$为整个存储器大小。、
2. ![alt text](image-42.png)
3. 搜索速度快，外部碎片少，但是有较大内部碎片
##### 可重定位分区分配
外部碎片大小总和可能已经超过了需求大小，但每个单独分区都不够。
1. 紧凑(compaction)：
   1. 将各个占用分区向一端移动，空出来较大的空闲空间![alt text](image-43.png)
   2. 移动会占用CPU时间，且需要额外硬件支持（重定位寄存器）
   3. 何时执行紧凑操作：每个分区释放后，或内存分配找不到满足条件的空闲分区时
   ![alt text](image-44.png)
2. 覆盖：目标是*在较小的可用内存中运行较大的程序*。常用于*多道程序系统*，与**固定分区存储管理**配合使用
   1. 将程序的重要常用模块常驻内存中；不常用模块放置在外存中，用到时才装入内存进行覆盖。不存在调用关系的模块没必要同时装入。
   2. 时间换空间，覆盖耗时；且编程时需要划分模块。
   3. **同一进程内**，只能覆盖与当前代码段无关的代码。
3. 对换(swapping，滚进，滚出)：
   1. 将主存中*暂时不能运行（阻塞、低优先级）的进程对换到外存*，腾出空闲空间来防止可以运行的进程或进程需要的数据等资源。
   2. 交换单位是*进程的整个地址空间*
   3. 外存被分为对换区和文件区，为了加快对换速度，os采用连续存储方式，少考虑碎片。
   4. *换出*:当前执行进程需要更多内存、创建了高优先级进程而内存不够时，os将阻塞态的低优先级进程传送至外村对换区；
   5. *换入*：内存空闲时，os将就绪且换出时间最久的进程传送至主存
   6. 可以增大并发数量，增大吞吐率；而对换过程耗时，且不考虑进程访问内存的统计特征。
   7. *不同进程间*
## 基本分页存储管理方式 
**离散地分配，基本单位是页**，不支持虚存技术，要求把整个作业都装入内存，才能运行。
1. 物理内存被划分为*固定大小（出厂设置）*的页框(page frame，物理页框，页帧)。进程的逻辑地址也被划分为多个页。
2. *逻辑地址映像*需要硬件（页表寄存器）支持。
3. 进程装入时寻找空闲页框（*不必连续*），进程每个页占据一个页框。![alt text](image-45.png)
4. 小页减少内碎片，但增大管理开销；大页相反。
5. 没有外碎片，内碎片小，程序不用顺序存放。但必须将整个程序都装入内存。
##### 基本分页管理中的数据结构
1. *物理页面表*：整个系统有一个，写明了*所有物理页框的分配使用情况*
2. *进程页表*：进程中的页表，写明了*进程中每页占用的物理页框号*。
![alt text](image-46.png)
3. *请求表*：整个系统一个，写明了*各个进程的进程页表位置和大小*，也可以放入PCB中，加载到页表寄存器后可以用于*物理地址映射*
##### 地址变换机构
1. 逻辑地址给出*逻辑页号，页内偏移*；查询进程页表可以找到对应的*物理页号*，通过业内偏移找到实际地址。
2. ![alt text](image-47.png)


   


