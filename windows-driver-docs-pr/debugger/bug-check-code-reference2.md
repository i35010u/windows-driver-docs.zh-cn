---
title: Bug 检查代码参考
description: 本部分包含常见错误检查的说明，包括传递到蓝屏的参数。
ms.assetid: DBA85578-97CF-4BD7-A67D-1C7AD2E9B2BB
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: b284c0beb6e4d7a60c59feed071e50f98c54e7ac
ms.sourcegitcommit: f91a0fd22f46be44839d2a22a21f59fad900ce90
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2019
ms.locfileid: "71020992"
---
# <a name="bug-check-code-reference"></a>Bug 检查代码参考

本部分包含常见 bug 检查代码的说明，包括在蓝色 bug 检查屏幕上用错误代码显示的参数。 本节还介绍如何诊断导致错误检查的错误，以及处理错误的可能方法。

> [!NOTE] 
> 本主题面向程序员。 如果你是其系统显示了带有 bug 检查代码的蓝屏的客户，请参阅[排查蓝屏错误](https://go.microsoft.com/fwlink/p/?linkid=183646)。

如果未在此引用中显示特定 bug 检查代码，请在 Windows 调试器（WinDbg）中使用 " [ **！分析**](-analyze.md)扩展" （在内核模式下），将替换`<code>`为 bug 检查代码：

`!analyze -show <code>`

输入此命令会导致 WinDbg 显示有关指定 bug 检查代码的信息。 如果默认数字基数（基数）不为16，则前缀`<code>`为**0x**。

下表显示了每个 bug 检查代码的代码和名称。

| 代码       | 名称                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000001 | [**APC\_索引\_不匹配**](bug-check-0x1--apc-index-mismatch.md)                                                                                  |
| 0x00000002 | [**设备\_队列\_不繁忙\_** ](bug-check-0x2--device-queue-not-busy.md)                                                                           |
| 0x00000003 | [**无效\_的\_地缘集**](bug-check-0x3--invalid-affinity-set.md)                                                                              |
| 0x00000004 | [**数据\_访问\_陷阱\_无效**](bug-check-0x4--invalid-data-access-trap.md)                                                                     |
| 0x00000005 | [**进程\_附加\_尝试\_无效**](bug-check-0x5--invalid-process-attach-attempt.md)                                                         |
| 0x00000006 | [**进程\_分离\_尝试\_无效**](bug-check-0x6--invalid-process-detach-attempt.md)                                                         |
| 0x00000007 | [**无效\_的\_软件中断**](bug-check-0x7--invalid-software-interrupt.md)                                                                  |
| 0x00000008 | [**IRQL\_不\_调度级别\_** ](bug-check-0x8--irql-not-dispatch-level.md)                                                                       |
| 0x00000009 | [**IRQL\_不\_大于或\_等于\_** ](bug-check-0x9--irql-not-greater-or-equal.md)                                                                  |
| 0x0000000A | [**IRQL\_不\_小于或\_等于\_** ](bug-check-0xa--irql-not-less-or-equal.md)                                                                        |
| 0x0000000B | [**无\_异常\_处理支持\_** ](bug-check-0xb--no-exception-handling-support.md)                                                           |
| 0x0000000C | [**超过\_最\_大\_等待对象数**](bug-check-0xc--maximum-wait-objects-exceeded.md)                                                           |
| 0x0000000D | [**互斥\_级别\_号冲突\_** ](bug-check-0xd--mutex-level-number-violation.md)                                                             |
| 0x0000000E | [**无\_用户\_模式上下文\_** ](bug-check-0xe--no-user-mode-context.md)                                                                             |
| 0x0000000F | [**旋转\_锁\_已拥有\_** ](bug-check-0xf--spin-lock-already-owned.md)                                                                       |
| 0x00000010 | [**旋转\_锁\_不归\_** ](bug-check-0x10--spin-lock-not-owned.md)                                                                              |
| 0x00000011 | [**线程\_非\_互斥体\_所有者**](bug-check-0x11--thread-not-mutex-owner.md)                                                                        |
| 0x00000012 | [**陷阱\_原因\_未知**](bug-check-0x12--trap-cause-unknown.md)                                                                                 |
| 0x00000013 | [**空\_线程\_REAPER列表\_** ](bug-check-0x13--empty-thread-reaper-list.md)                                                                    |
| 0x00000014 | [**未\_\_\_锁定创建删除锁定\_** ](bug-check-0x14--create-delete-lock-not-locked.md)                                                         |
| 0x00000015 | [**上次\_从\_KMODE调用\_的机会\_** ](bug-check-0x15--last-chance-called-from-kmode.md)                                                         |
| 0x00000016 | [**CID\_句\_柄创建**](bug-check-0x16--cid-handle-creation.md)                                                                               |
| 0x00000017 | [**CID\_句\_柄删除**](bug-check-0x17--cid-handle-deletion.md)                                                                               |
| 0x00000018 | [ **\_通过\_指针引用**](bug-check-0x18--reference-by-pointer.md)                                                                             |
| 0x00000019 | [**错误\_的\_池标头**](bug-check-0x19--bad-pool-header.md)                                                                                       |
| 0x0000001A | [**内存\_管理**](bug-check-0x1a--memory-management.md)                                                                                    |
| 0x0000001B | [**PFN\_共享\_计数**](bug-check-0x1b--pfn-share-count.md)                                                                                       |
| 0x0000001C | [**PFN\_引用\_计数**](bug-check-0x1c--pfn-reference-count.md)                                                                               |
| 0x0000001D | [**没有\_可用\_的\_旋转锁**](bug-check-0x1d--no-spin-lock-available.md)                                                                        |
| 0x0000001E | [ **\_未\_处理KMODE\_异常**](bug-check-0x1e--kmode-exception-not-handled.md)                                                              |
| 0x0000001F | [**共享\_资源\_约定错误\_** ](bug-check-0x1f--shared-resource-conv-error.md)                                                                |
| 0x00000020 | [**在\_退出期间\_\_内核APC\_挂起**](bug-check-0x20--kernel-apc-pending-during-exit.md)                                                       |
| 0x00000021 | [**配额\_下溢**](bug-check-0x21--quota-underflow.md)                                                                                        |
| 0x00000022 | [**文件\_系统**](bug-check-0x22--file-system.md)                                                                                                |
| 0x00000023 | [**FAT\_文件\_系统**](bug-check-0x23--fat-file-system.md)                                                                                       |
| 0x00000024 | [**NTFS\_文件\_系统**](bug-check-0x24--ntfs-file-system.md)                                                                                     |
| 0x00000025 | [**NPFS\_文件\_系统**](bug-check-0x25--npfs-file-system.md)                                                                                     |
| 0x00000026 | [**CDFS\_文件\_系统**](bug-check-0x26--cdfs-file-system.md)                                                                                     |
| 0x00000027 | [**RDR\_文件\_系统**](bug-check-0x27--rdr-file-system.md)                                                                                       |
| 0x00000028 | [**损坏\_的\_访问令牌**](bug-check-0x28--corrupt-access-token.md)                                                                             |
| 0x00000029 | [**安全\_系统**](bug-check-0x29--security-system.md)                                                                                        |
| 0x0000002A | [**IRP\_不一致**](bug-check-0x2a--inconsistent-irp.md)                                                                                      |
| 0x0000002B | [**紧急\_堆栈\_开关**](bug-check-0x2b--panic-stack-switch.md)                                                                                 |
| 0x0000002C | [**内部\_端口\_驱动程序**](bug-check-0x2c--port-driver-internal.md)                                                                             |
| 0x0000002D | [**SCSI\_磁盘\_驱动程序\_内部**](bug-check-0x2d--scsi-disk-driver-internal.md)                                                                  |
| 0x0000002E | [**数据\_总线\_错误**](bug-check-0x2e--data-bus-error.md)                                                                                         |
| 0x0000002F | [**指令\_总线\_错误**](bug-check-0x2f--instruction-bus-error.md)                                                                           |
| 0x00000030 | [**一\_组\_无效\_的上下文**](bug-check-0x30--set-of-invalid-context.md)                                                                        |
| 0x00000031 | [**阶段 0\_初始化\_失败**](bug-check-0x31--phase0-initialization-failed.md)                                                             |
| 0x00000032 | [**阶段 1\_初始化\_失败**](bug-check-0x32--phase1-initialization-failed.md)                                                             |
| 0x00000033 | [**意外\_的\_初始化调用**](bug-check-0x33--unexpected-initialization-call.md)                                                         |
| 0x00000034 | [**缓存\_管理器**](bug-check-0x34--cache-manager.md)                                                                                            |
| 0x00000035 | [**没有\_更\_多IRP\_堆栈位置\_** ](bug-check-0x35--no-more-irp-stack-locations.md)                                                             |
| 0x00000036 | [**设备\_引用\_计数\_不为\_零**](bug-check-0x36--device-reference-count-not-zero.md)                                                     |
| 0x00000037 | [**软盘\_内部\_错误**](bug-check-0x37--floppy-internal-error.md)                                                                           |
| 0x00000038 | [**内部\_串行\_驱动程序**](bug-check-0x38--serial-driver-internal.md)                                                                         |
| 0x00000039 | [**系统\_出口\_拥有\_的 MUTEX**](bug-check-0x39--system-exit-owned-mutex.md)                                                                      |
| 0x0000003A | [**系统\_展开\_前一个\_用户**](bug-check-0x3a--system-unwind-previous-user.md)                                                              |
| 0x0000003B | [**系统\_服务\_异常**](bug-check-0x3b--system-service-exception.md)                                                                     |
| 0x0000003C | [**尝试\_中断\_展开**](bug-check-0x3c--interrupt-unwind-attempted.md)                                                                 |
| 0x0000003D | [**中断\_异常\_未处理\_** ](bug-check-0x3d--interrupt-exception-not-handled.md)                                                      |
| 0x0000003E | [ **\_不\_支持多处理器\_配置**](bug-check-0x3e--multiprocessor-configuration-not-supported.md)                                |
| 0x0000003F | [**无\_更\_多系统\_PTE**](bug-check-0x3f--no-more-system-ptes.md)                                                                              |
| 0x00000040 | [**目标\_MDL\_太小\_** ](bug-check-0x40--target-mdl-too-small.md)                                                                            |
| 0x00000041 | [**必须\_成功\_池\_为空**](bug-check-0x41--must-succeed-pool-empty.md)                                                                      |
| 0x00000042 | [**ATDISK\_驱动\_程序内部**](bug-check-0x42--atdisk-driver-internal.md)                                                                         |
| 0x00000043 | [**无\_此\_分区**](bug-check-0x43--no-such-partition.md)                                                                                   |
| 0x00000044 | [**多\_IRP\_完成请求\_** ](bug-check-0x44--multiple-irp-complete-requests.md)                                                        |
| 0x00000045 | [**系统\_映射\_REGS\_不足**](bug-check-0x45--insufficient-system-map-regs.md)                                                            |
| 0x00000046 | [**DEREF\_未知\_登录会话\_** ](bug-check-0x46--deref-unknown-logon-session.md)                                                              |
| 0x00000047 | [**引用\_未知\_登录会话\_** ](bug-check-0x47--ref-unknown-logon-session.md)                                                                  |
| 0x00000048 | [**已\_完成\_\_IRP中的取消状态\_** ](bug-check-0x48--cancel-state-in-completed-irp.md)                                                         |
| 0x00000049 | [**中断\_中断\_的\_页面错误\_** ](bug-check-0x49--page-fault-with-interrupts-off.md)                                                       |
| 0x0000004A | [**系统\_\_\_服务上\_的 IRQL GT 0\_** ](bug-check-0x4a--irql-gt-zero-at-system-service.md)                                                      |
| 0x0000004B | [**流\_内部\_错误**](bug-check-0x4b--streams-internal-error.md)                                                                         |
| 0x0000004C | [**严重\_的\_未\_处理硬错误**](bug-check-0x4c--fatal-unhandled-hard-error.md)                                                                |
| 0x0000004D | [**无\_可用\_页面**](bug-check-0x4d--no-pages-available.md)                                                                                 |
| 0x0000004E | [**PFN\_列表\_已损坏**](bug-check-0x4e--pfn-list-corrupt.md)                                                                                     |
| 0x0000004F | [**NDIS\_内部\_错误**](bug-check-0x4f--ndis-internal-error.md)                                                                               |
| 0x00000050 | [**非\_分页\_\_区域中的页面错误\_** ](bug-check-0x50--page-fault-in-nonpaged-area.md)                                                             |
| 0x00000051 | [**注册表\_错误**](bug-check-0x51--registry-error.md)                                                                                          |
| 0x00000052 | [**MAILSLOT\_文件\_系统**](bug-check-0x52--mailslot-file-system.md)                                                                             |
| 0x00000053 | [**无\_启动\_设备**](bug-check-0x53--no-boot-device.md)                                                                                         |
| 0x00000054 | [**LM\_服务器\_内部错误\_** ](bug-check-0x54--lm-server-internal-error.md)                                                                    |
| 0x00000055 | [**数据\_一致性\_异常**](bug-check-0x55--data-coherency-exception.md)                                                                     |
| 0x00000056 | [**指令\_一致性\_异常**](bug-check-0x56--instruction-coherency-exception.md)                                                       |
| 0x00000057 | [**XNS\_内部\_错误**](bug-check-0x57--xns-internal-error.md)                                                                                 |
| 0x00000058 | [**FTDISK\_内部\_错误**](bug-check-0x58--ftdisk-internal-error.md)                                                                           |
| 0x00000059 | [**弹球\_文件\_系统**](bug-check-0x59--pinball-file-system.md)                                                                               |
| 0x0000005A | [**关键\_服务\_失败**](bug-check-0x5a--critical-service-failed.md)                                                                       |
| 0x0000005B | [**设置\_ENV\_VAR失败\_** ](bug-check-0x5b--set-env-var-failed.md)                                                                                |
| 0x0000005C | [**HAL\_初始化\_失败**](bug-check-0x5c--hal-initialization-failed.md)                                                                   |
| 0x0000005D | [**处理器\_不受支持**](bug-check-0x5d--unsupported-processor.md)                                                                            |
| 0x0000005E | [**对象\_初始化\_失败**](bug-check-0x5e--object-initialization-failed.md)                                                             |
| 0x0000005F | [**安全\_初始化\_失败**](bug-check-0x5f--security-initialization-failed.md)                                                         |
| 0x00000060 | [**进程\_初始化\_失败**](bug-check-0x60--process-initialization-failed.md)                                                           |
| 0x00000061 | [**HAL1\_初始化\_失败**](bug-check-0x61--hal1-initialization-failed.md)                                                                 |
| 0x00000062 | [**OBJECT1\_初始化\_失败**](bug-check-0x62--object1-initialization-failed.md)                                                           |
| 0x00000063 | [**SECURITY1\_初始化\_失败**](bug-check-0x63--security1-initialization-failed.md)                                                       |
| 0x00000064 | [**符号\_初始化\_失败**](bug-check-0x64--symbolic-initialization-failed.md)                                                         |
| 0x00000065 | [**MEMORY1\_初始化\_失败**](bug-check-0x65--memory1-initialization-failed.md)                                                           |
| 0x00000066 | [**缓存\_初始化\_失败**](bug-check-0x66--cache-initialization-failed.md)                                                               |
| 0x00000067 | [**配置\_初始化\_失败**](bug-check-0x67--config-initialization-failed.md)                                                             |
| 0x00000068 | [**文件\_初始化\_失败**](bug-check-0x68--file-initialization-failed.md)                                                                 |
| 0x00000069 | [**IO1\_初始化\_失败**](bug-check-0x69--io1-initialization-failed.md)                                                                   |
| 0x0000006A | [**LPC\_初始化\_失败**](bug-check-0x6a--lpc-initialization-failed.md)                                                                   |
| 0x0000006B | [**PROCESS1\_初始化\_次数**](bug-check-0x6b--process1-initialization-failed.md)D                                                         |
| 0x0000006C | [**REFMON\_初始化\_失败**](bug-check-0x6c--refmon-initialization-failed.md)                                                             |
| 0x0000006D | [**SESSION1\_初始化\_失败**](bug-check-0x6d--session1-initialization-failed.md)                                                         |
| 0x0000006E | [**SESSION2\_初始化\_失败**](bug-check-0x6e--session2-initialization-failed.md)                                                         |
| 0x0000006F | [**SESSION3\_初始化\_失败**](bug-check-0x6f--session3-initialization-failed.md)                                                         |
| 0x00000070 | [**SESSION4\_初始化\_失败**](bug-check-0x70--session4-initialization-failed.md)                                                         |
| 0x00000071 | [**SESSION5\_初始化\_失败**](bug-check-0x71--session5-initialization-failed.md)                                                         |
| 0x00000072 | [**分配\_驱动器\_号失败\_** ](bug-check-0x72--assign-drive-letters-failed.md)                                                              |
| 0x00000073 | [**配置\_列表\_失败**](bug-check-0x73--config-list-failed.md)                                                                                 |
| 0x00000074 | [**系统\_配置\_信息\_错误**](bug-check-0x74--bad-system-config-info.md)                                                                        |
| 0x00000075 | [**无法\_写入\_配置**](bug-check-0x75--cannot-write-configuration.md)                                                                 |
| 0x00000076 | [**进程\_已\_锁定页面\_** ](bug-check-0x76--process-has-locked-pages.md)                                                                    |
| 0x00000077 | [**内核\_堆栈\_INPAGE错误\_** ](bug-check-0x77--kernel-stack-inpage-error.md)                                                                  |
| 0x00000078 | [**阶段 0\_异常**](bug-check-0x78--phase0-exception.md)                                                                                      |
| 0x00000079 | [**不\_匹配 HAL**](bug-check-0x79--mismatched-hal.md)                                                                                          |
| 0x0000007A | [**内核\_数据\_INPAGE错误\_** ](bug-check-0x7a--kernel-data-inpage-error.md)                                                                    |
| 0x0000007B | [ **\_启动\_设备不可访问**](bug-check-0x7b--inaccessible-boot-device.md)                                                                     |
| 0x0000007C | [**BUGCODE\_NDIS\_驱动程序**](bug-check-0x7c--bugcode-ndis-driver.md)                                                                               |
| 0x0000007D | [**安装\_更\_多内存**](bug-check-0x7d--install-more-memory.md)                                                                               |
| 0x0000007E | [**系统\_线程\_异常未\_处理\_** ](bug-check-0x7e--system-thread-exception-not-handled.md)                                             |
| 0x0000007F | [**意外\_的\_内核模式\_陷阱**](bug-check-0x7f--unexpected-kernel-mode-trap.md)                                                              |
| 0x00000080 | [**NMI\_硬件\_故障**](bug-check-0x80--nmi-hardware-failure.md)                                                                             |
| 0x00000081 | [**旋转\_锁\_初始化失败\_** ](bug-check-0x81--spin-lock-init-failure.md)                                                                        |
| 0x00000082 | [**DFS\_文件\_系统**](bug-check-0x82--dfs-file-system.md)                                                                                       |
| 0x00000085 | [**安装\_失败**](bug-check-0x85--setup-failure.md)                                                                                            |
| 0x0000008B | [**MBR\_校验\_和不匹配**](bug-check-0x8b--mbr-checksum-mismatch.md)                                                                           |
| 0x0000008E | [**未\_\_\_处理内核模式异常\_** ](bug-check-0x8e--kernel-mode-exception-not-handled.md)                                                 |
| 0x0000008F | [**PP0\_初始化\_失败**](bug-check-0x8f--pp0-initialization-failed.md)                                                                   |
| 0x00000090 | [**PP1\_初始化\_失败**](bug-check-0x90--pp1-initialization-failed.md)                                                                   |
| 0x00000092 | [**MP\_\_\_系统上的驱动程序\_** ](bug-check-0x92--up-driver-on-mp-system.md)                                                                       |
| 0x00000093 | [ **\_内核\_句柄无效**](bug-check-0x93--invalid-kernel-handle.md)                                                                           |
| 0x00000094 | [**在\_退出\_时锁定\_的\_内核堆栈**](bug-check-0x94--kernel-stack-locked-at-exit.md)                                                             |
| 0x00000096 | [**工作\_队列\_项\_无效**](bug-check-0x96--invalid-work-queue-item.md)                                                                      |
| 0x00000097 | [**不\_支持\_绑定映像**](bug-check-0x97--bound-image-unsupported.md)                                                                       |
| 0x00000098 | [ **\_NT\_评估期结束\_\_** ](bug-check-0x98--end-of-nt-evaluation-period.md)                                                             |
| 0x00000099 | [**无效\_的\_区域或\_段**](bug-check-0x99--invalid-region-or-segment.md)                                                                  |
| 0x0000009A | [**系统\_许可证\_冲突**](bug-check-0x9a--system-license-violation.md)                                                                     |
| 0x0000009B | [**UDF\_文件\_系统**](bug-check-0x9b--udfs-file-system.md)                                                                                     |
| 0x0000009C | [**计算机\_检查\_异常**](bug-check-0x9c--machine-check-exception.md)                                                                       |
| 0x0000009E | [**用户\_模式\_运行状况\_监视器**](bug-check-0x9e--user-mode-health-monitor.md)                                                                    |
| 0x0000009F | [**驱动\_程序\_电源状态\_故障**](bug-check-0x9f--driver-power-state-failure.md)                                                                |
| 0x000000A0 | [**内部\_电源\_错误**](bug-check-0xa0--internal-power-error.md)                                                                             |
| 0x000000A1 | [**PCI\_总线\_驱动程序\_内部**](bug-check-0xa1--pci-bus-driver-internal.md)                                                                      |
| 0x000000A2 | [**内存\_映像\_已损坏**](bug-check-0xa2--memory-image-corrupt.md)                                                                             |
| 0x000000A3 | [**ACPI\_驱动\_程序内部**](bug-check-0xa3--acpi-driver-internal.md)                                                                             |
| 0x000000A4 | [**CNSS\_文件\_系统\_筛选器**](bug-check-0xa4--cnss-file-system-filter.md)                                                                      |
| 0x000000A5 | [**ACPI\_BIOS\_错误**](bug-check-0xa5--acpi-bios-error.md)                                                                                       |
| 0x000000A7 | [**错误\_的 EXHANDLE**](bug-check-0xa7--bad-exhandle.md)                                                                                              |
| 0x000000AB | [**会话\_在\_退出\_时\_具有有效的池\_** ](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x000000AC | [**HAL\_内存\_分配**](bug-check-0xac--hal-memory-allocation.md)                                                                           |
| 0x000000AD | [**视频\_驱动\_程序调试\_报表请求\_** ](bug-check-0xad--video-driver-debug-report-request.md)                                                 |
| 0x000000B1 | [**BGI\_检测\_到冲突**](bug-check-0xb1--bgi-detected-violation.md)                                                                         |
| 0x000000B4 | [**视频\_驱动\_程序初始化\_失败**](bug-check-0xb4--video-driver-init-failure.md)                                                                  |
| 0x000000B8 | [**尝试\_\_从DPC\_切换**](bug-check-0xb8--attempted-switch-from-dpc.md)                                                                  |
| 0x000000B9 | [**芯片组\_检测\_到错误**](bug-check-0xb9--chipset-detected-error.md)                                                                         |
| 0x000000BA | [**会话\_在\_退出\_时\_具有有效的视图\_** ](bug-check-0xba--session-has-valid-views-on-exit.md)                                                    |
| 0x000000BB | [**网络\_启动\_初始化失败\_** ](bug-check-0xbb--network-boot-initialization-failed.md)                                                |
| 0x000000BC | [**网络\_启动\_重复地址\_** ](bug-check-0xbc--network-boot-duplicate-address.md)                                                        |
| 0x000000BD | [ **\_休眠\_状态无效**](bug-check-0xbd--invalid-hibernated-state.md)                                                                     |
| 0x000000BE | [**尝试\_写入\_只读\_内存\_** ](bug-check-0xbe--attempted-write-to-readonly-memory.md)                                               |
| 0x000000BF | [**互斥\_体\_已拥有**](bug-check-0xbf--mutex-already-owned.md)                                                                               |
| 0x000000C1 | [**特殊\_池\_检测到\_内存损坏\_** ](bug-check-0xc1--special-pool-detected-memory-corruption.md)                                     |
| 0x000000C2 | [**错误\_的\_池调用方**](bug-check-0xc2--bad-pool-caller.md)                                                                                       |
| 0x000000C4 | [**驱动\_程序\_验证\_程序检测到冲突**](bug-check-0xc4--driver-verifier-detected-violation.md)                                                |
| 0x000000C5 | [**驱动\_程序\_损坏 EXPOOL**](bug-check-0xc5--driver-corrupted-expool.md)                                                                       |
| 0x000000C6 | [**已\_捕获驱动\_程序修改\_已释放\_的便便**](bug-check-0xc6--driver-caught-modifying-freed-pool.md)L                                               |
| 0x000000C7 | [**计时器\_或\_DPC无效\_** ](bug-check-0xc7--timer-or-dpc-invalid.md)                                                                            |
| 0x000000C8 | [**IRQL\_意外\_值**](bug-check-0xc8--irql-unexpected-value.md)                                                                           |
| 0x000000C9 | [**驱动\_程序\_验证\_器 IOMANAGER 冲突**](bug-check-0xc9--driver-verifier-iomanager-violation.md)                                              |
| 0x000000CA | [**PNP\_\_检测到错误\_** ](bug-check-0xca--pnp-detected-fatal-error.md)                                                                    |
| 0x000000CB | [ **\_驱动程序已锁定\_页面\_正在\_处理\_** ](bug-check-0xcb--driver-left-locked-pages-in-process.md)                                            |
| 0x000000CC | [**释放\_\_\_的特殊池中\_的页错误\_** ](bug-check-0xcc--page-fault-in-freed-special-pool.md)                                                  |
| 0x000000CD | [**超出\_\_分配结束\_的页面\_错误\_** ](bug-check-0xcd--page-fault-beyond-end-of-allocation.md)                                            |
| 0x000000CE | [**已\_卸载\_\_驱动程序，\_无需取消挂起的操作\_** ](bug-check-0xce--driver-unloaded-without-cancelling-pending-operations.md)        |
| 0x000000CF | [**终端\_服务器\_驱动程序\_进行了\_错误\_的内存引用\_** ](bug-check-0xcf--terminal-server-driver-made-incorrect-memory-reference.md)     |
| 0x000000D0 | [**驱动\_程序\_损坏 MMPOOL**](bug-check-0xd0--driver-corrupted-mmpool.md)                                                                       |
| 0x000000D1 | [**驱动\_程序\_IRQL不\_小于\_或等于\_** ](bug-check-0xd1--driver-irql-not-less-or-equal.md)                                                        |
| 0x000000D2 | [**BUGCODE\_ID\_驱动程序**](bug-check-0xd2--bugcode-id-driver.md)                                                                                   |
| 0x000000D3 | [**驱动\_程序\_部分必须\_未分页\_** ](bug-check-0xd3--driver-portion-must-be-nonpaged.md)                                                     |
| 0x000000D4 | [**引发\_\_的\_IRQL系统扫描导致驱动程序卸载\_不正确\_\_\_\_** ](bug-check-0xd4--system-scan-at-raised-irql-caught-improper-driver-unlo.md) |
| 0x000000D5 | [**已\_释放\_的特殊\_池中的\_驱动程序页错误\_\_** ](bug-check-0xd5--driver-page-fault-in-freed-special-pool.md)                                   |
| 0x000000D6 | [**超出\_\_\_分配结束\_的驱动\_程序页错误\_** ](bug-check-0xd6--driver-page-fault-beyond-end-of-allocation.md)                             |
| 0x000000D7 | [**驱动\_程序\_取消\_映射无效视图**](bug-check-0xd7--driver-unmapping-invalid-view.md)                                                          |
| 0x000000D8 | [**驱动\_程序\_使用\_过多 PTE**](bug-check-0xd8--driver-used-excessive-ptes.md)                                                                |
| 0x000000D9 | [**锁定\_页面\_跟踪\_器损坏**](bug-check-0xd9--locked-pages-tracker-corruption.md)                                                      |
| 0x000000DA | [**系统\_PTE\_盗用**](bug-check-0xda--system-pte-misuse.md)                                                                                   |
| 0x000000DB | [**驱动\_程序\_损坏 SYSPTES**](bug-check-0xdb--driver-corrupted-sysptes.md)                                                                     |
| 0x000000DC | [**驱动\_程序\_堆栈\_访问无效**](bug-check-0xdc--driver-invalid-stack-access.md)                                                              |
| 0x000000DE | [**文件\_\_\_区域中的池损坏\_** ](bug-check-0xde--pool-corruption-in-file-area.md)                                                           |
| 0x000000DF | 我[**模拟\_工作线程\_** ](bug-check-0xdf--impersonating-worker-thread.md)                                                               |
| 0x000000E0 | [**ACPI\_\_BIOS 错误\_** ](bug-check-0xe0--acpi-bios-fatal-error.md)                                                                          |
| 0x000000E1 | [**错误\_\_的IRQL\_返回的\_工作线程\_** ](bug-check-0xe1--worker-thread-returned-at-bad-irql.md)                                              |
| 0x000000E2 | [**手动\_启动\_崩溃**](bug-check-0xe2--manually-initiated-crash.md)                                                                     |
| 0x000000E3 | [**资源\_不\_拥有**](bug-check-0xe3--resource-not-owned.md)                                                                                 |
| 0x000000E4 | [**辅助\_角色无效**](bug-check-0xe4--worker-invalid.md)                                                                                          |
| 0x000000E6 | [**驱动\_程序\_验证\_程序 DMA 冲突**](bug-check-0xe6--driver-verifier-dma-violation.md)                                                          |
| 0x000000E7 | [ **\_浮点\_状态无效\_** ](bug-check-0xe7--invalid-floating-point-state.md)                                                            |
| 0x000000E8 | [**无效\_的\_文件打开\_取消\_** ](bug-check-0xe8--invalid-cancel-of-file-open.md)                                                             |
| 0x000000E9 | [**活动\_EX\_工作线程\_终止\_** ](bug-check-0xe9--active-ex-worker-thread-termination.md)                                             |
| 0x000000EA | [**设备\_\_\_驱动程序中的线程停滞\_** ](bug-check-0xea--thread-stuck-in-device-driver.md)                                                         |
| 0x000000EB | [**脏\_映射\_页拥塞\_** ](bug-check-0xeb--dirty-mapped-pages-congestion.md)                                                          |
| 0x000000EC | [**会话\_在\_退出\_时\_具有有效的特殊池\_\_** ](bug-check-0xec--session-has-valid-special-pool-on-exit.md)                                     |
| 0x000000ED | [**无法\_装入\_启动卷**](bug-check-0xed--unmountable-boot-volume.md)                                                                       |
| 0x000000EF | [**关键\_进程\_终止**](bug-check-0xef--critical-process-died.md)                                                                           |
| 0x000000F0 | [**存储\_微型\_端口错误**](bug-check-0xf0--storage-miniport-error.md)                                                                         |
| 0x000000F1 | [**检测到\_\_SCSI验证器\_冲突**](bug-check-0xf1--scsi-verifier-detected-violation.md)                                                    |
| 0x000000F2 | [**硬件\_中断\_风暴**](bug-check-0xf2--hardware-interrupt-storm.md)                                                                     |
| 0x000000F3 | [**DISORDERLY\_关闭**](bug-check-0xf3--disorderly-shutdown.md)                                                                                |
| 0x000000F4 | [**关键\_对象\_终止**](bug-check-0xf4--critical-object-termination.md)                                                               |
| 0x000000F5 | [**FLTMGR\_文件\_系统**](bug-check-0xf5--fltmgr-file-system.md)                                                                                 |
| 0x000000F6 | [**PCI\_\_验证\_程序检测到冲突**](bug-check-0xf6--pci-verifier-detected-violation.md)                                                      |
| 0x000000F7 | [**驱动\_程序\_OVERRAN堆栈\_缓冲区**](bug-check-0xf7--driver-overran-stack-buffer.md)                                                              |
| 0x000000F8 | [**RAMDISK\_启动\_初始化失败\_** ](bug-check-0xf8--ramdisk-boot-initialization-failed.md)                                                |
| 0x000000F9 | [**驱动\_程序\_返回\_了\_卷\_打开状态的重新分析\_** ](bug-check-0xf9--driver-returned-status-reparse-for-volume-open.md)                     |
| 0x000000FA | [**HTTP\_驱动\_程序已损坏**](bug-check-0xfa---http-driver-corrupted.md)                                                                          |
| 0x000000FC | [**尝试\_执行\_NOEXECUTE\_内存\_** ](bug-check-0xfc---attempted-execute-of-noexecute-memory.md)                                        |
| 0x000000FD | [**脏\_NOWRITE\_PAGES拥塞\_** ](bug-check-0xfd---dirty-nowrite-pages-congestion.md)                                                       |
| 0x000000FE | [**BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)                                                                                 |
| 0x000000FF | [**保留\_队列\_溢出**](bug-check-0xff---reserve-queue-overflow.md)                                                                        |
| 0x00000100 | [**加载\_程序\_块不匹配**](bug-check-0x100---loader-block-mismatch.md)                                                                         |
| 0x00000101 | [**时钟\_监视\_程序超时**](bug-check-0x101---clock-watchdog-timeout.md)                                                                       |
| 0x00000102 | [**DPC\_监视\_程序超时**](bug-check-0x102--dpc-watchdog-timeout.md)                                                                            |
| 0x00000103 | [**MUP\_文件\_系统**](bug-check-0x103---mup-file-system.md)                                                                                     |
| 0x00000104 | [**AGP\_无效\_访问**](bug-check-0x104---agp-invalid-access.md)                                                                               |
| 0x00000105 | [**AGP\_GART\_损坏**](bug-check-0x105---agp-gart-corruption.md)                                                                             |
| 0x00000106 | [**AGP\_非法\_REPROGRAMMED**](bug-check-0x106---agp-illegally-reprogrammed.md)                                                               |
| 0x00000108 | [**第\_三\_方文件\_系统失败\_** ](bug-check-0x108--third-party-file-system-failure.md)                                                    |
| 0x00000109 | [**关键\_结构\_损坏**](bug-check-0x109---critical-structure-corruption.md)                                                         |
| 0x0000010A | [**应用\_标记\_初始化失败\_** ](bug-check-0x10a---app-tagging-initialization-failed.md)                                                |
| 0x0000010C | [**FSRTL\_额外\_的CREATE\_参数冲突\_** ](bug-check-0x10c---fsrtl-extra-create-parameter-violation.md)                                     |
| 0x0000010D | [**WDF\_冲突**](bug-check-0x10d---wdf-violation.md)                                                                                          |
| 0x0000010E | [**内部\_视频\_内存管理\_** ](bug-check-0x10e---video-memory-management-internal.md)                                                  |
| 0x0000010F | [**资源\_管理\_器异常\_未处理\_** ](bug-check-0x10f---resource-manager-exception-not-handled.md)                                     |
| 0x00000111 | [**递归\_NMI**](bug-check-0x111---recursive-nmi.md)                                                                                          |
| 0x00000112 | [**MSRPC\_状态\_冲突**](bug-check-0x112---msrpc-state-violation.md)                                                                         |
| 0x00000113 | [**视频\_\_DXGKRNL 错误\_** ](bug-check-0x113---video-dxgkrnl-fatal-error.md)                                                                |
| 0x00000114 | [**视频\_阴影\_驱动程序\_错误\_** ](bug-check-0x114---video-shadow-driver-fatal-error.md)                                                   |
| 0x00000115 | [**AGP\_内部**](bug-check-0x115---agp-internal.md)                                                                                            |
| 0x00000116 | [**视频\_TDR\_故障**](bug-check-0x116---video-tdr-failure.md)                                                                                     |
| 0x00000117 | [**检测\_到\_视频\_TDR 超时**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000119 | [**视频\_计划\_程序内部\_错误**](bug-check-0x119---video-scheduler-internal-error.md)                                                      |
| 0x0000011A | [**EM\_初始化\_失败**](bug-check-0x11a---em-initialization-failure.md)                                                                 |
| 0x0000011B | [**驱动\_程序\_返回保存\_取消锁定\_** ](bug-check-0x11b---driver-returned-holding-cancel-lock.md)                                           |
| 0x0000011C | [**已\_尝试\_写入\_到CM\_保护的\_存储**](bug-check-0x11c--attempted-write-to-cm-protected-storage.md)                                   |
| 0x0000011D | [**事件\_跟踪\_严重错误\_** ](bug-check-0x11d---event-tracing-fatal-error.md)                                                                |
| 0x0000011E | [ **\_递归\_错误太\_多**](bug-check-0x11e--too-many-recursive-faults.md)                                                                |
| 0x0000011F | [**驱动\_程序\_句柄无效**](bug-check-0x11f--invalid-driver-handle.md)                                                                         |
| 0x00000120 | [**BITLOCKER\_严重\_错误**](bug-check-0x120--bitlocker-fatal-error-.md)                                                                        |
| 0x00000121 | [**驱动\_程序冲突**](bug-check-0x121---driver-violation.md)                                                                                    |
| 0x00000122 | [**WHEA\_内部\_错误**](bug-check-0x122---whea-internal-error.md)                                                                             |
| 0x00000123 | [**加密\_\_自检失败\_** ](bug-check-0x123--crypto-self-test-failure-.md)                                                                 |
| 0x00000124 | [**WHEA\_无法\_纠正的错误**](bug-check-0x124---whea-uncorrectable-error.md)                                                                   |
| 0x00000125 | [**NMR\_无效\_状态**](bug-check-0x125--nmr-invalid-state.md)                                                                                 |
| 0x00000126 | [**NETIO\_无效\_的池\_调用方**](bug-check-0x126--netio-invalid-pool-caller.md)                                                                |
| 0x00000127 | [**页\_不\_为零**](bug-check-0x127---page-not-zero.md)                                                                                         |
| 0x00000128 | [**返回\_的工作\_线程\_具有错误\_的 IO\_优先级\_** ](bug-check-0x128--worker-thread-returned-with-bad-io-priority.md)                          |
| 0x00000129 | [**返回\_\_\_了错误\_分页IO\_优先级的\_工作线程\_** ](bug-check-0x129--worker-thread-returned-with-bad-paging-io-priority.md)           |
| 0x0000012A | [**MUI\_没有\_有效的\_系统语言\_** ](bug-check-0x12a--mui-no-valid-system-language.md)                                                          |
| 0x0000012B | [**错误\_的\_硬件损坏\_页**](bug-check-0x12b---faulty-hardware-corrupted-page.md)                                                      |
| 0x0000012C | [**EXFAT\_文件\_系统**](bug-check-0x12c---exfat-file-system.md)                                                                                 |
| 0x0000012D | [**VOLSNAP\_重叠\_表访问\_** ](bug-check-0x12d--volsnap-overlapped-table-access.md)                                                     |
| 0x0000012E | [ **\_MDL\_范围无效**](bug-check-0x12e--invalid-mdl-range.md)                                                                                  |
| 0x0000012F | [**VHD\_启动\_初始化失败\_** ](bug-check-0x12f--vhd-boot-initialization-failed.md)                                                       |
| 0x00000130 | [**动态\_添加\_处理器\_不匹配**](bug-check-0x130--dynamic-add-processor-mismatch.md)                                                       |
| 0x00000131 | [**扩展\_处理器\_状态\_无效**](bug-check-0x131--invalid-extended-processor-state.md)                                                   |
| 0x00000132 | [**资源\_所有者\_指针无效\_** ](bug-check-0x132--resource-owner-pointer-invalid.md)                                                       |
| 0x00000133 | [**DPC\_监视\_程序冲突**](bug-check-0x133-dpc-watchdog-violation.md)                                                                         |
| 0x00000134 | [**驱动器\_扩展器**](bug-check-0x134--drive-extender.md)                                                                                         |
| 0x00000135 | [**注册表\_筛选\_器\_驱动程序异常**](bug-check-0x135--registry-filter-driver-exception.md)                                                   |
| 0x00000136 | [**VHD\_启动\_主机\_卷空间不足\_\_\_** ](bug-check-0x136--vhd-boot-host-volume-not-enough-space.md)                                      |
| 0x00000137 | [**WIN32K.SYS\_句\_柄管理器**](bug-check-0x137--win32k-handle-manager.md)                                                                          |
| 0x00000138 | [**GPIO\_控制器\_驱动程序\_错误**](bug-check-0x138-gpio-controller-driver-error.md)                                                            |
| 0x00000139 | [**内核\_安全\_检查失败\_** ](bug-check-0x139--kernel-security-check-failure.md)                                              |
| 0x0000013A | [**内核\_模式\_堆损坏\_** ](bug-check-0x13a--kernel-mode-heap-corruption.md)                                                             |
| 0x0000013B | [**被动\_中断\_错误**](bug-check-0x13b--passive-interrupt-error.md)                                                                      |
| 0x0000013C | [**IO\_提升\_状态\_无效**](bug-check-0x13c--invalid-io-boost-state.md)                                                                       |
| 0x0000013D | [**关键\_初始化\_失败**](bug-check-0x13d--critical-initialization-failure.md)                                                      |
| 0x00000140 | [**检测\_到\_存储\_设备异常情况**](bug-check-0x140--storage-device-abnormality-detected.md)                                             |
| 0x00000141 | [**检测\_到\_视频\_引擎超时**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**已\_阻止\_视频\_TDR 应用程序**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000143 | [**处理器\_驱动\_程序内部**](bug-check-0x143--processor-driver-internal.md)                                                                  |
| 0x00000144 | [**BUGCODE\_USB3\_驱动程序**](bug-check-0x144--bugcode-usb3-driver.md)                                                                              |
| 0x00000145 | [**安全\_启动\_冲突**](bug-check-0x145--secure-boot-violation-.md)                                                                         |
| 0x00000147 | [**检测\_到\_异常重置**](bug-check-0x147--abnormal-reset-detected.md)                                                                      |
| 0x00000149 | [**REFS\_文件\_系统**](bug-check-0x149--refs-file-system.md)                                                                                    |
| 0x0000014A | [**内核\_WMI\_内部**](bug-check-0x14a--kernel-wmi-internal.md)                                                                              |
| 0x0000014B | [**SOC\_子系统\_故障**](bug-check-0x14b--soc-subsystem-failure.md)                                                                          |
| 0x0000014C | [**致命\_异常\_重置\_错误**](bug-check-0x14c--fatal-abnormal-reset-error.md)                                                               |
| 0x0000014D | [**异常\_范围\_无效**](bug-check-0x14d--exception-scope-invalid.md)                                                                      |
| 0x0000014E | [**已\_删除\_SOC\_严重设备**](bug-check-0x14e--soc-critical-device-removed.md)                                                             |
| 0x0000014F | [**PDC\_监视\_程序超时**](bug-check-0x14f--pdc-watchdog-timeout.md)                                                                            |
| 0x00000150 | [**TCPIP\_AOAC\_NIC\_活动引用泄露\_\_** ](bug-check-0x150--tcpip-aoac-nic-active-reference-leak.md)                                         |
| 0x00000151 | [**不\_受\_支持的指令模式**](bug-check-0x151--unsupported-instruction-mode.md)                                                            |
| 0x00000152 | [**推送\_锁定\_标记\_无效**](bug-check-0x152--invalid-push-lock-flags.md)                                                                     |
| 0x00000153 | [**线程\_\_\_终止时\_泄漏内核\_锁定条目\_** ](bug-check-0x153--kernel-lock-entry-leaked-on-thread-termination.md)                    |
| 0x00000154 | [**意外\_的\_存储异常**](bug-check-0x154--unexpected-store-exception.md)                                                                |
| 0x00000155 | [**操作系统\_数据\_篡改**](bug-check-0x155--os-data-tampering.md)                                                                                  |
| 0x00000156 | [**WINSOCK\_检测\_到挂起\_导致LIVEDUMP\_** ](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x00000157 | [**内核\_线程\_优先级底价\_违规\_** ](bug-check-0x157--kernel-thread-priority-floor-violation.md)                                      |
| 0x00000158 | [**非法\_的\_IOMMU页面\_错误**](bug-check-0x158--illegal-iommu-page-fault.md)                                                                   |
| 0x00000159 | [**HAL\_非法\_的IOMMU\_页面错误\_** ](bug-check-0x159--hal-illegal-iommu-page-fault.md)                                                          |
| 0x0000015A | [**SDBUS\_内部\_错误**](bug-check-0x15a--sdbus-internal-error.md)                                                                            |
| 0x0000015B | [**返回\_\_系统\_页面优先级的\_工作线程处于活动状态\_\_\_** ](bug-check-0x15b--worker-thread-returned-with-system-page-priority-active.md) |
| 0x0000015C | [**PDC\_监视\_程序超时\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)              
| 0x0000015D | [**SOC\_子系统\_故障LIVEDUMP\_** ](bug-check-0x15d-soc-subsystem-failure-livedump.md)              
| 0x0000015E | [**BUGCODE\_NDIS\_驱动程序\_实时转储\_** ](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**连接\_备用\_监视器超时\_LIVEDUMP\_** ](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000160 | [**WIN32K.SYS\_原子\_检查失败\_** ](bug-check-0x160--win32k-atomic-check-failure.md)                                                             |
| 0x00000161 | [**实时\_系统\_转储**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000162 | [**内核\_自动\_提升无效\_的锁定\_版本\_** ](bug-check-0x162--kernel-auto-boost-invalid-lock-release.md)                                     |
| 0x00000163 | [**工作\_线程\_测试条件\_** ](bug-check-0x162--worker-thread-test-condition.md)                                                           |
| 0x00000164 | [**WIN32K.SYS\_严重\_故障**](bug-check-0x164--win32k-critical-failure.md)                                                                      |
| 0x00000165 | [**群集\_CSV\_状态\_IO超时LIVEDUMP\_\_** ](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      | 
| 0x00000166 | [**群集\_资源\_调用超时\_LIVEDUMP\_** ](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**群集\_CSV\_快照设备\_信息\_超时LIVEDUMP\_\_** ](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |    
| 0x00000168 | [**群集\_CSV\_状态\_转换超时LIVEDUMP\_\_** ](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**群集\_CSV\_卷到达\_LIVEDUMP\_** ](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**群集\_CSV\_卷删除\_LIVEDUMP\_** ](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**群集\_CSV\_群集\_监视程序\_LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                       |   
| 0x0000016C | [**断开\_保护\_标志\_无效**](bug-check-0x16c--invalid-rundown-protection-flags.md)                                                   |
| 0x0000016D | [**槽\_分配\_器标记\_无效**](bug-check-0x16d--invalid-slot-allocator-flags.md)                                                           |
| 0x0000016E | [**ERESOURCE\_无效\_版本**](bug-check-0x16e--eresource-invalid-release.md)                                                                  |
| 0x0000016F | [**群集\_CSV\_状态转换\_间隔\_超时LIVEDUMP\_\_** ](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000170 | [**加密\_库\_内部错误\_** ](bug-check-0x170--crypto-library-internal-error.md)                                                         |
| 0x00000171 | [**群集\_CSV\_CLUSSVC断开\_连接监视器\_** ](bug-check-0x171--cluster-csv-clussvc-disconnect-watchdog.md)                                    |
| 0x00000173 | [**COREMSGCALL\_内部\_错误**](bug-check-0x173--coremsgcall-internal-error.md)                                                                |
| 0x00000174 | [**COREMSG\_内部\_错误**](bug-check-0x174--coremsg-internal-error.md)                                                                        |
| 0x00000175 | [**上\_一个\_严重\_的\_异常重置错误**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000178 | [**ELAM\_驱动\_程序\_检测到\_错误**](bug-check-0x175--elam-driver-detected-fatal-error.md)                                                  |
| 0x00000179 | [**群集\_CLUSPORT\_状态\_IO超时LIVEDUMP\_\_** ](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017B | [**探查\_器\_配置非法**](bug-check-0x17b--profiler-configuration-illegal.md)                                                        | 
| 0x0000017C | [**PDC\_锁\_监视\_程序 LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_意外\_吊销LIVEDUMP\_** ](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x0000017E | [**微码\_版本\_不匹配**](bug-check-0x17e--microcode-revision-mismatch.md)                                                              | 
| 0x00000187 | [**视频\_DWMINIT\_超时回退\_BDD\_** ](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**群集\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000189 | [**错误\_的\_对象标头**](bug-check-0x189--bad-object-header.md)                                                                                  |
| 0x0000018B | [**安全\_内核\_错误**](bug-check-0x18b--secure-kernel-error.md)                                                                              |
| 0x0000018C | [**HYPERGUARD\_冲突**](bug-check-0x18c--hyperguard-violation.md)                                                                              |   
| 0x0000018D | [**未\_处理\_安全错误**](bug-check-0x18d--secure-fault-unhandled.md)                                                                        | 
| 0x0000018E | [**内核\_分区\_引用冲突\_** ](bug-check-0x18e--kernel-partition-reference-violation.md)                                           |
| 0x00000190 | [**WIN32K.SYS\_严重\_故障LIVEDUMP\_** ](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000191 | [**PF\_检测\_到损坏**](bug-check-0x191--pf-detected-corruption.md)                                                                        |
| 0x00000192 | [**内核\_自动\_提升锁\_获取，\_引发了\_IRQL\_\_** ](bug-check-0x192--kernel-auto-boost-lock-acquisition-with-raised-irql.md)         |
| 0x00000193 | [**视频\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_服务器\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000196 | [**检测\_到\_加载程序回滚**](bug-check-0x196--loader-rollback-detected.md)                                                                    |
| 0x00000197 | [**WIN32K.SYS\_安全\_故障**](bug-check-0x197--win32k-security-failure.md)                                                                      |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x00000199 | [**内核\_存储\_槽正在\_使用中\_** ](bug-check-0x199--kernel-storage-slot-in-use.md)                                                              |
| 0x0000019A | [**附加\_\_\_到接收器时\_返回的\_工作线程\_** ](bug-check-0x19a--worker-thread-returned-while-attached-to-silo.md)                      |
| 0x0000019B | [**TTM\_错误\_** ](bug-check-0x19b--ttm-fatal-error.md)                                                                                      |
| 0x0000019C | [**WIN32K.SYS\_POWER\_监视器超时\_** ](bug-check-0x19c--win32k-power-watchdog-timeout.md)                                                         |
| 0x0000019D | [**CLUSTER\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A0 | [**TTM\_监视器\_超时**](bug-check-0x1a0--ttm-watchdog-timeout.md)                                                                            |
| 0x000001A3 | [ **\_调用\_未返回监视\_程序超时LIVEDUMP\_\_\_** ](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW发散\_LIVEDUMP\_** ](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_阻止人\_兴奋删除\_LIVEDUMP\_** ](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**蓝牙\_错误\_恢复LIVEDUMP\_** ](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_重\_定向程序 LIVEDUMP**](bug-check-0x1A7--smb-redirector-livedump.md)                                                                       |
| 0x000001A8 | [**视频\_DXGKRNL\_黑屏幕\_LIVEDUMP\_** ](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001C4 | [**驱动\_程序\_验证\_程序\_检测到冲突 LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_线程\_池\_死锁 LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C6 | [**快速\_ERESOURCE\_前置条件\_冲突**](bug-check-0x1c6--fast-eresource-precondition-violation.md)                                         |
| 0x000001C7 | [**存储\_数据\_结构损坏\_** ](bug-check-0x1c7--store-data-structure-corruption.md)                                                     |
| 0x000001C8 | [**手动\_启动\_的电源\_按钮保留\_** ](bug-check-0x1c8--manually-initiated-power-button-hold.md)                                          |
| 0x000001C9 | [**用户\_模式\_运行状况\_监视器LIVEDUMP\_** ](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CA | [**综合\_监视\_程序超时**](bug-check-0x1ca--synthetic-watchdog-timeout.md)                                                                |
| 0x000001CB | [ **\_接收器\_分离无效**](bug-check-0x1cb--invalid-silo-detach.md)                                                                              |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001CD | [**无效\_的\_回调 STACK_ADDRESS**](bug-check-0x1cd--invalid-callback-stack-address.md)                                                        |
| 0x000001CE | [**内核\_堆栈\_地址\_无效**](bug-check-0x1ce--invalid-kernel-stack-address.md)                                                           |
| 0x000001CF | [**硬件\_监视\_程序超时**](bug-check-0x1cf--hardware-watchdog-timeout.md)                                                                  |  
| 0x000001D0 | [**CPI\_固件\_监视器超时\_** ](bug-check-0x1d0--acpi-firmware-watchdog-timeout.md)                                                        |
| 0x000001D1 | [**遥测\_断言\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D2 | [**工作\_\_线程\_的状态无效**](bug-check-0x1d2--worker-thread-invalid-state.md)                                                             |
| 0x000001D3 | [**WFP\_无效\_操作**](bug-check-0x1d3--wfp-invalid-operation.md)                                                                          |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |
| 0x000001D5 | [**DRIVER_PNP_WATCHDOG**](bug-check-0x1d5--driver-pnp-watchdog.md)                                                                                |
| 0x000001D6 | [**返回\_\_的工作\_线程包含非\_默认工作负荷\_类\_\_** ](bug-check-0x1d6--worker-thread-returned-with-non-default-workload-class.md)   |
| 0x000001D7 | [**EFS\_严重\_错误**](bug-check-0x1d7--efs-fatal-error.md)                                                                                      |
| 0x000001D8 | [**UCMUCSI\_失败**](bug-check-0x1d8--ucmucsi-failure.md)                                                                                       |
| 0x000001D9 | [**HAL\_IOMMU\_内部错误\_** ](bug-check-0x1d8--ucmucsi-failure.md)                                                                            |
| 0x000001DB | [**IPI\_监视\_程序超时**](bug-check-0x1db--ipi-watchdog-timeout.md)                                                                            |
| 0x000001DC | [**DMA_COMMON_BUFFER_VECTOR_ERROR**](bug-check-0x1dc--dma-common-buffer-vector-error.md)                                                          |
| 0x00000356 | [**XBOX\_ERACTRL\_CS超时\_** ](bug-check-0x356--xbox-eractrl-cs-timeout.md)                                                                     |
| 0x00000BFE | [**BC\_蓝牙\_验证\_程序错误**](bug-check-0xbfe--bc-bluetooth-verifier-fault.md)                                                             |
| 0x00000BFF | [**BC\_BTHMINI\_验证\_程序错误**](bug-check-0xbff--bc-bthmini-verifier-fault.md)                                                                 |
| 0x00020001 | [**虚拟\_机监控程序错误**](bug-check-0x20001--hypervisor-error.md)                                                                                   |
| 0x1000007E | [**系统\_线程\_异常\_未处理M\_\_** ](bug-check-0x1000007e--system-thread-exception-not-handled-m.md)                                  |
| 0x1000007F | [**意外\_的\_内核模式\_陷阱M\_** ](bug-check-0x1000007f--unexpected-kernel-mode-trap-m.md)                                                   |
| 0x1000008E | [**内核\_模式\_异常\_未处理M\_\_** ](bug-check-0x1000008e--kernel-mode-exception-not-handled-m.md)                                      |
| 0x100000EA | [**线程\_\_停滞在设备\_驱动程序\_M 中\_** ](bug-check-0x100000ea--thread-stuck-in-device-driver-m.md)                                              |
| 0x4000008A | [**线程\_终止\_持有\_互斥体**](bug-check-0x4000008a--thread-terminate-held-mutex.md)                                                        |
| 0xC0000218 | [**状态\_无法\_加载注册表\_文件\_** ](bug-check-0xc0000218--status-cannot-load-registry-file.md)                                             |
| 0xC000021A | [**WINLOGON\_严重\_错误**](bug-check-0xc000021a--winlogin-fatal-error.md)                                              |
| 0xC0000221 | [**状态\_映像\_校验和\_不匹配**](bug-check-0xc0000221--status-image-checksum-mismatch.md)                                                  |
| 0xDEADDEAD | [**手动\_启动\_的 CRASH1**](bug-check-0xdeaddead--manually-initiated-crash1.md)                                                             |
