.. 数据保护实验:

---------------------
数据保护实验
---------------------

概览
++++++++

Nutanix提供了VM / vDisk的存储快照的功能。保护域（PD）是用于对VM进行分组以及应用快照和复制策略的结构。

在本练习中，您将使用Prism对VM实现快照的创建和还原，以及为VM创建保护域。

数据保护
+++++++++++++++

虚拟机快照
............

#. 在 **Prism Element > VM > 列表中**, 选择您的 *Initials*-**Linux_VM** VM.

#. 如果虚拟机已启动，请执行 **Guest Shutdown** 电源操作.

#. 选择虚拟机，然后从表下方的菜单中单击 **Take Snapshot** .

#. 为您的快照提供一个名称，然后单击 **Submit**.

#. 选择表下方的 **VM Snapshots** 选项卡以查看所选虚拟机的可用快照.

   .. figure:: images/manage_workloads_04.png

#. 在 **Actions**, 下，单击 **Details** 以查看快照时虚拟机的所有属性.

   您可以看到快照不仅包含其数据，还包含VM状态.

   *现在是时候断开您的虚拟机了!*

#. 单击 **Update** 以修改您的VM，并通过单击每个项目的 **X** 图标来删除CD-ROM和磁盘.

#. 点击 **Save**.

#. 尝试启动VM并启动其控制台窗口.

   请注意，VM不再具有要从中引导的任何磁盘，并且显示 2048 游戏.

#. 关闭虚拟机电源.

#. 在 **VM Snapshots**, 选择您的快照，然后单击 **Restore** 以将虚拟机恢复为正常运行状态.

   或者，您可以单击 **Clone** 以还原到新的VM.

#. 验证虚拟机是否成功启动.

如前所述，Nutanix快照使用的写重定向<https://nutanixbible.com/#anchor-book-of-acropolis-snapshots-and-clones>`_ 方法不会遭受在其他管理程序中找到的链接快照.

保护域
..................

#. 在 **Prism Element > Data Protection > Table**, 点击 **+ Protection Domain > Async DR** 以开始创建PD.

   .. 注意::

      当前在ESXi上支持同步复制（Metro可用性）。将来的版本将在AHV中支持它.

#. 打开菜单的“数据保护”上下文时，将显示警告屏幕。单击 **OK** 按钮前进.

 .. figure:: images/data_protection_01.png

#. 提供PD的名称，然后单击 **Create**.

#. 筛选或滚动以选择要在此练习中创建的要添加到PD的VM.

#. 单击 **Protect Selected Entities** 并验证VM是否显示在 **Protected Entities**.

   一致性组可让您将多个VM分组为同一快照，例如属于同一应用程序的多个VM.

   .. 注意:: Nutanix快照可以为安装了NGT的受支持操作系统执行与应用程序一致的快照。使用应用程序一致性快照的每个VM将成为其自己的一致性组的一部分.

#. 点击 **Next**.

#. 点击 **New Schedule** 以定义恢复点目标（RPO）和保留.

#. 配置所需的快照频率（例如，每1小时重复一次）

   .. 注意::

      AHV支持NearSync快照，RPO低至1分钟.

   .. 注意::

      可以将多个计划应用于同一PD，从而使您可以获取和保留X个小时的每小时，每天，每月快照.

#. 配置保留策略（例如保留最后5张快照）

   .. 注意::

      对于配置了远程群集的环境，设置复制就像定义每个远程站点上保留多少快照一样简单.

      .. figure:: images/snapshot_02.png

#. 点击 **Create Schedule**.

#. 点击 **Close** 退出.

可在 `此处 <https://nutanixbible.com/#anchor-book-of-acropolis-backup-and-disaster-recovery>`_找到更多信息.

您已经在Prism中成功配置了本机数据保护.

结论
+++++++++

- Nutanix通过不同的策略（包括一对一或一对多复制）为虚拟数据中心提供数据保护解决方案.
- Nutanix在VM，文件和卷组级别提供了数据保护功能，因此VM和数据在崩溃一致的环境中保持安全.
- 可以通过Prism对任何受支持的管理程序进行VM级快照和复制策略的管理.
