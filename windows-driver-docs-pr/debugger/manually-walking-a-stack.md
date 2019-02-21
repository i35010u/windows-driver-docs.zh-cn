---
title: 手动遍历堆栈
description: 手动遍历堆栈
ms.assetid: 9235fe4d-3e94-4143-867f-18b696e489d0
keywords:
- 堆栈跟踪，手动遍历堆栈
- 遍历堆栈
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcb994d4b0641161ecf7c3bd7bdf7a6af253609e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521054"
---
# <a name="manually-walking-a-stack"></a>手动遍历堆栈


## <span id="ddk_manually_walking_a_stack_dbg"></span><span id="DDK_MANUALLY_WALKING_A_STACK_DBG"></span>


在某些情况下，堆栈跟踪函数将无法在调试器中。 这可能引起对无效的地址导致调试器无法继续的位置返回的地址; 的调用或您可能会遇到不能直接获得的堆栈跟踪; 的堆栈指针或者，可能有一些其他调试器问题。 在任何情况下，能够手动遍历堆栈通常是有价值的。

基本概念是相当简单： 转储堆栈指针、 已加载模块发现、 查找可能的函数地址，并通过检查以查看每个可能的堆栈项是是否通过到下一个调用来验证。

之前通过一个示例，务必要注意[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令在 Intel 系统上有另一项功能。 通过执行 kb =\[ebp\] \[eip\] \[esp\]，调试器将显示在帧的堆栈跟踪替换为基的指针、 指令指针和堆栈指针的给定值分别。

。 例如，因此结果可以检查结束时使用失败引起的实际上可以在堆栈跟踪。

第一步是找出哪些模块加载的位置。 这通过实现[ **（检查符号） x** ](x--examine-symbols-.md) （某些符号编辑长度性的） 的命令：

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

第二步转储出要查找由给定的模块中的地址的堆栈指针**x \*！** 命令：

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

若要确定哪些值是可能的函数地址以及不参数或保存的寄存器，首先要考虑的是不同类型的信息在堆栈上的类似。 大多数整数将较小值，这意味着它们将通常为零 （如 0x00000270) 显示为 dword 值时。 大多数本地地址的指针将堆栈指针 （如 fe4cca78) 旁。 状态代码通常以 c (c00000d6) 开头。 可以通过每个字符将在 20 7f 的范围内的事实识别 Unicode 和 ASCII 字符串。 (KD，在[ **dc （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令将显示在右侧的字符。)按列出的范围的函数地址将是最重要的是， **x \*！**。

请注意，列出的所有模块到 8040 c 000 77f70000 和到 fe6f0920 fe4c0000 的范围内。 根据这些范围，上述列表中的可能的函数地址是：80136039，801036fe (两次列出，因此更有可能参数)，fe682ae4，fe68f57a，fe682a78，fe6a1198，8011 c 901，80127797、 80110008，fe6a1430，fe6a10ae，fe6b2c04，fe685968，fe680ba4，和 fe682050。 使用检查这些位置[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令用于每个地址：

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

如前面提到的 801036fe 很可能不是堆栈跟踪的一部分如列出两次。 如果返回的地址偏移量为零，也可以忽略 （您不能返回到函数的开头）。 根据此信息，堆栈跟踪显示为：

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

若要验证每个符号，反汇编指定若要查看它是否按其上方的函数调用的返回地址之前。 若要减少长度，请编辑以下 （通过试用和错误来找到使用的偏移量）：

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

此基础，显示的**RdrReconnectConnection**称为**RdrCleanupTransportConnection**到**RdrTdiDisconnect**到**ZwCloseObjectAuditAlarm**到**KiSystemServiceExit**。 在堆栈上的其他函数是可能的剩余部分之前处于活动状态的堆栈。

在这种情况下，堆栈跟踪都将正常工作。 下面是实际的堆栈跟踪以检查答案：

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

第一个条目是当前位置基于堆栈跟踪，但为堆栈直到正确位置**RdrReconnectConnection**调用。 可以使用相同的过程来跟踪整个堆栈。 有关更精确的手动堆栈审核方法，将需要反汇编潜在的每个函数，然后按照每个**推送**并**pop**来标识在堆栈上的每个 DWORD。

 

 





