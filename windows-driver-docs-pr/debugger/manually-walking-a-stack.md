---
title: 手动遍历堆栈
description: 手动遍历堆栈
keywords:
- 堆栈跟踪，手动遍历堆栈
- 遍历堆栈
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e5a6af4c32ee115bd7de42fedfdf3b3a35823ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814559"
---
# <a name="manually-walking-a-stack"></a>手动遍历堆栈


## <span id="ddk_manually_walking_a_stack_dbg"></span><span id="DDK_MANUALLY_WALKING_A_STACK_DBG"></span>


在某些情况下，堆栈跟踪函数在调试器中将失败。 这可能是由于调用了导致调试器丢失返回地址位置的无效地址所致;或者，您可能遇到过无法直接获取堆栈跟踪的堆栈指针;否则可能存在其他一些调试程序问题。 在任何情况下，都可以手动遍历堆栈，这通常很有价值。

基本概念非常简单：转储堆栈指针，找出模块的加载位置，查找可能的函数地址，并通过检查每个可能的堆栈条目是否调用下一个。

在执行示例之前，请务必注意， [**kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令在 Intel 系统上具有其他功能。 通过执行 kb = \[ ebp \] \[ eip \] \[ \] ，调试程序将分别显示带有给定的基指针、指令指针和堆栈指针值的帧的堆栈跟踪。

在此示例中，将使用实际提供堆栈跟踪的失败，以便可以在结束时检查结果。

第一步是找出加载的模块。 这是通过 [**x (检查符号)**](x--examine-symbols-.md) 命令完成的， (出于长度) 的原因，编辑某些符号：

```dbgcmd
kd> x *! 
start    end        module name
77f70000 77fb8000   ntdll     (C:\debug\ntdll.dll, \\ntstress\symbols\dll\ntdll.DBG)
80010000 80012320   Aha154x   (load from Aha154x.sys deferred)
80013000 8001aa60   SCSIPORT  (load from SCSIPORT.SYS deferred)
8001b000 8001fba0   Scsidisk  (load from Scsidisk.sys deferred)

80100000 801b7b40   NT        (ntoskrnl.exe, \\ntstress\symbols\exe\ntoskrnl.DBG)
802f0000 8033c000   Ntfs      (load from Ntfs.sys deferred)
80400000 8040c000   hal       (load from hal.dll deferred)
fe4c0000 fe4c38c0   vga       (load from vga.sys deferred)
fe4d0000 fe4d3e60   VIDEOPRT  (load from VIDEOPRT.SYS deferred)
fe4e0000 fe4f0e40   ati       (load from ati.SYS deferred)
fe500000 fe5057a0   Msfs      (load from Msfs.SYS deferred)
fe510000 fe519560   Npfs      (load from Npfs.SYS deferred)

fe520000 fe521f60   ndistapi  (load from ndistapi.sys deferred)
fe530000 fe54ed20   Fastfat   (load from Fastfat.SYS deferred)
fe5603e0 fe575360   NDIS      (NDIS.SYS, \\ntstress\symbols\SYS\NDIS.DBG)
fe580000 fe585920   elnkii    (elnkii.sys, \\ntstress\symbols\sys\elnkii.DBG)
fe590000 fe59b8a0   ndiswan   (load from ndiswan.sys deferred)
fe5a0000 fe5b7c40   nbf       (load from nbf.sys deferred)
fe5c0000 fe5c1b40   TDI       (load from TDI.SYS deferred)
fe5d0000 fe5dd580   nwlnkipx  (load from nwlnkipx.sys deferred)

fe5e0000 fe5ee220   nwlnknb   (load from nwlnknb.sys deferred)
fe5f0000 fe5fb320   afd       (load from afd.sys deferred)
fe610000 fe62bf00   tcpip     (load from tcpip.sys deferred)
fe630000 fe648600   netbt     (load from netbt.sys deferred)
fe650000 fe6572a0   netbios   (load from netbios.sys deferred)
fe660000 fe660000   Parport   (load from Parport.SYS deferred)
fe670000 fe670000   Parallel  (load from Parallel.SYS deferred)
fe680000 fe6bcf20   rdr       (rdr.sys, \\ntstress\symbols\sys\rdr.DBG)

fe6c0000 fe6f0920   srv       (load from srv.sys deferred) 
```

第二步是转储堆栈指针，查找 **x \*** 所提供的模块中的地址。 命令：

```dbgcmd
kd> dd esp 
fe4cc97c  80136039 00000270 00000000 00000000
fe4cc98c  fe682ae4 801036fe 00000000 fe68f57a
fe4cc99c  fe682a78 ffb5b030 00000000 00000000
fe4cc9ac  ff680e08 801036fe 00000000 00000000
fe4cc9bc  fe6a1198 00000001 fe4cca78 ffae9d98

fe4cc9cc  02000901 fe4cca68 ffb50030 ff680e08
fe4cc9dc  ffa449a8 8011c901 fe4cca78 00000000
fe4cc9ec  80127797 80110008 00000246 fe6a1430

kd> dd 
fe4cc9fc  00000270 fe6a10ae 00000270 ffa44abc
fe4cca0c  ffa449a8 ff680e08 fe6b2c04 ff680e08
fe4cca1c  ffa449a8 e12820c8 e1235308 ffa449a8
fe4cca2c  fe685968 ff680e08 e1235308 ffa449a8
fe4cca3c  ffb0ad48 ffb0ad38 00100000 ffb0ad38
fe4cca4c  00000000 ffa44a84 e1235308 0000000a
fe4cca5c  c00000d6 00000000 004ccb28 fe4ccbc4

fe4cca6c  fe680ba4 fe682050 00000000 fe4ccbd4 
```

若要确定哪些值很可能是函数地址以及哪些是参数或保存的寄存器，首先要考虑不同类型的信息在堆栈上的外观。 大多数整数将是较小的值，这意味着，当 0x00000270)  (时，它们将大部分为零。 指向本地地址的大多数指针都将接近堆栈指针 (如 fe4cca78) 。 状态代码通常以 c (c00000d6) 开始。 Unicode 和 ASCII 字符串可以通过这一事实标识，因为每个字符都将在7f 范围内。  (在 KD 中， [**dc (显示 Memory)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令将在右侧显示字符。 ) 最重要的是，函数地址将在 **x \* ！** 列出的范围内。

请注意，列出的所有模块都位于77f70000 到8040c000 和 fe4c0000 到 fe6f0920 的范围内。 根据这些范围，前面列出的可能的函数地址为：80136039、801036fe (列出两次，因此更有可能是参数) 、fe682ae4、fe68f57a、fe682a78、fe6a1198、8011c901、80127797、80110008、fe6a1430、fe6a10ae、fe6b2c04、fe685968、fe680ba4 和 fe682050。 使用 ln (列出每个地址的 [**最接近符号)**](ln--list-nearest-symbols-.md) 命令来调查这些位置：

```dbgcmd
kd> ln 80136039 
(80136039)   NT!_KiServiceExit+0x1e  |  (80136039)   NT!_KiServiceExit2-0x177
kd> ln fe682ae4 
(fe682ae4)   rdr!_RdrSectionInfo+0x2c | (fe682ae4)   rdr!_RdrFcbReferenceLock-0xb4
kd> ln 801036fe 
(801036fe)   NT!_KeWaitForSingleObject | (801036fe)   NT!_MmProbeAndLockPages-0x2f8
kd> ln fe68f57a 
(fe68f57a)   rdr!_RdrDereferenceDiscardableCode+0xb4  
                         (fe68f57a)   rdr!_RdrUninitializeDiscardableCode-0xa
kd> ln fe682a78 
(fe682a78)   rdr!_RdrDiscardableCodeLock | (fe682a78) rdr!_RdrDiscardableCodeTimeout-0x38

kd> ln fe6a1198 
(fe6a1198)   rdr!_SubmitTdiRequest+0xae | (fe6a1198)   rdr!_RdrTdiAssociateAddress-0xc
kd> ln 8011c901 
(8011c901)   NT!_KeSuspendThread+0x13 | (8011c901)   NT!_FsRtlCheckLockForReadAccess-0x55
kd> ln 80127797 
(80127797)   NT!_ZwCloseObjectAuditAlarm+0x7 | (80127797)   NT!_ZwCompleteConnectPort-0x9
kd> ln 80110008 
(80110008)   NT!_KeWaitForMultipleObjects+0x27c | (80110008) NT!_FsRtlLookupMcbEntry-0x164
kd> ln fe6a1430 
(fe6a1430)   rdr!_RdrTdiCloseConnection+0xa | (fe6a1430)   rdr!_RdrDoTdiConnect-0x4

kd> ln fe6a10ae 
(fe6a10ae)   rdr!_RdrTdiDisconnect+0x56 | (fe6a10ae)   rdr!_SubmitTdiRequest-0x3c
kd> ln fe6b2c04 
(fe6b2c04)   rdr!_CleanupTransportConnection+0x64 | (fe6b2c04)rdr!_RdrReferenceServer-0x20
kd> ln fe685968 
(fe685968)   rdr!_RdrReconnectConnection+0x1b6
                        (fe685968)   rdr!_RdrInvalidateServerConnections-0x32
kd> ln fe682050 
(fe682050)   rdr!__strnicmp+0xaa  |  (fe682050)   rdr!_BackPackSpinLock-0xa10 
```

如前所述，801036fe 不太可能是堆栈跟踪的一部分，因为它列出了两次。 如果返回地址的偏移量为零，则可以将其忽略， (无法返回到函数) 的开头。 基于此信息，堆栈跟踪如下所示：

```dbgcmd
NT!_KiServiceExit+0x1e
rdr!_RdrSectionInfo+0x2c
rdr!_RdrDereferenceDiscardableCode+0xb4  
rdr!_SubmitTdiRequest+0xae
NT!_KeSuspendThread+0x13
NT!_ZwCloseObjectAuditAlarm+0x7
NT!_KeWaitForMultipleObjects+0x27c
rdr!_RdrTdiCloseConnection+0xa
rdr!_RdrTdiDisconnect+0x56
rdr!_CleanupTransportConnection+0x64
rdr!_RdrReconnectConnection+0x1b6
rdr!__strnicmp+0xaa 
```

若要验证每个符号，请在指定的返回地址之前立即 unassemble，以查看它是否对其上方的函数进行调用。 若要缩短长度，请将以下内容编辑 (通过试用和错误) 找到的偏移量：

```dbgcmd
kd> u 80136039-2 l1      //  looks ok, its a call
NT!_KiServiceExit+0x1c:
80136037 ffd3             call    ebx
kd> u fe682ae4-2 l1      //  paged out (all zeroes) unknown
rdr!_RdrSectionInfo+0x2a:
fe682ae2 0000             add     [eax],al
kd> u fe68f57a-6 l1      //  looks ok, its a call, but not anything above
rdr!_RdrDereferenceDiscardableCode+0xae:
fe68f574 ff15203568fe     call dword ptr [rdr!__imp__ExReleaseResourceForThreadLite]
kd> u fe682a78-6 l1      //  paged out (all zeroes) unknown

rdr!_DiscCodeInitialized+0x2:
fe682a72 0000             add     [eax],al
kd> u  fe6a1198-5 l1      //  looks good, call to something above
rdr!_SubmitTdiRequest+0xa9:
fe6a1193 e82ee3feff       call  rdr!_RdrDereferenceDiscardableCode (fe68f4c6)
kd> u 8011c901-2 l1      //  not good, its a jump in the function
NT!_KeSuspendThread+0x11:
8011c8ff 7424             jz      NT!_KeSuspendThread+0x37 (8011c925)
kd> u 80127797-2 l1      //  looks good, an int 2e -> KiServiceExit

NT!_ZwCloseObjectAuditAlarm+0x5:
80127795 cd2e             int     2e
kd> u 80110008-2 l1      //  not good, its a test instruction not a call
NT!_KeWaitForMultipleObjects+0x27a:
80110006 85c9             test    ecx,ecx
kd> u 80110008-5 l1      //  paged out (all zeroes) unknown
NT!_KeWaitForMultipleObjects+0x277:
80110003 0000             add     [eax],al
kd> u fe6a1430-6 l1      //  looks good its a call to ZwClose...
rdr!_RdrTdiCloseConnection+0x4:
fe6a142a ff15f83468fe     call    dword ptr [rdr!__imp__ZwClose (fe6834f8)]

kd> u fe6a10ae-2 l1      //  paged out (all zeroes) unknown
rdr!_RdrTdiDisconnect+0x54:
fe6a10ac 0000             add     [eax],al
kd> u  fe6b2c04-5 l1      //  looks good, call to something above
rdr!_CleanupTransportConnection+0x5f:
fe6b2bff e854e4feff       call    rdr!_RdrTdiDisconnect (fe6a1058)
kd> u fe685968-5 l1      //  looks good, call to immediately above
rdr!_RdrReconnectConnection+0x1b1:
fe685963 e838d20200       call    rdr!_CleanupTransportConnection (fe6b2ba0)

kd> u fe682050-2 l1      //  paged out (all zeroes) unknown
rdr!__strnicmp+0xa8:
fe68204e 0000             add     [eax],al 
```

基于这一点，似乎 **RdrReconnectConnection** 名为 **RdrCleanupTransportConnection**、 **RdrTdiDisconnect**、 **ZwCloseObjectAuditAlarm** 和 **KiSystemServiceExit**。 堆栈上的其他函数可能是之前处于活动状态的堆栈的遗留部分。

在这种情况下，堆栈跟踪会正常运行。 下面是用于检查答案的实际堆栈跟踪：

```dbgcmd
kd> k 
ChildEBP RetAddr
fe4cc978 80136039 NT!_NtClose+0xd
fe4cc978 80127797 NT!_KiServiceExit+0x1e

fe4cc9f4 fe6a1430 NT!_ZwCloseObjectAuditAlarm+0x7
fe4cca10 fe6b2c04 rdr!_RdrTdiCloseConnection+0xa
fe4cca28 fe685968 rdr!_CleanupTransportConnection+0x64
fe4cca78 fe688157 rdr!_RdrReconnectConnection+0x1b6
fe4ccbd4 80106b1e rdr!_RdrFsdCreate+0x45b
fe4ccbe8 8014b289 NT!IofCallDriver+0x38
fe4ccc98 8014decd NT!_IopParseDevice+0x693
fe4ccd08 8014d6d2 NT!_ObpLookupObjectName+0x487
fe4ccde4 8014d3ad NT!_ObOpenObjectByName+0xa2
fe4cce90 8016660d NT!_IoCreateFile+0x433
fe4cced0 80136039 NT!_NtCreateFile+0x2d 
```

第一项是基于堆栈跟踪的当前位置，否则堆栈会正确地定位到调用 **RdrReconnectConnection** 的点。 可以使用相同的过程跟踪整个堆栈。 若要获得更精确的手动堆栈遍历方法，需要 unassemble 每个潜在函数并按照每个 **推送** 和 **pop** 来识别堆栈上的每个 DWORD。

 

 





