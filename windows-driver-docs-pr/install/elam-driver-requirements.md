---
title: ELAM 驱动程序要求
description: 驱动程序安装必须使用现有工具进行联机和脱机安装，注册通过典型 INF 处理驱动程序。
ms.assetid: B00B4361-B531-4D28-A521-0F8B3B48CEA4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 005cc3daaee4e66308dbbfea2e97782b4f2d7963
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546407"
---
# <a name="elam-driver-requirements"></a>ELAM 驱动程序要求


驱动程序安装必须使用现有工具进行联机和脱机安装，注册通过典型 INF 处理驱动程序。  有关示例 ELAM 驱动程序代码，请参阅： https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam 

## <a name="am-driver-installation"></a>将驱动程序安装


若要确保驱动程序安装兼容性，ELAM 驱动程序将公布自己为类似于其他所有引导启动驱动程序的引导启动驱动程序。 INF 将启动类型设置为 SERVICE_BOOT_START (0)，指示应启动加载程序加载和初始化内核初始化期间，驱动程序。 ELAM 驱动程序公布其组为"初期启动"。 下一节中所述，将在 Windows 中，实现此组中的驱动程序的早期启动行为。

下面是一个 ELAM 驱动程序 INF 驱动程序安装部分的示例。

```cpp
[SampleAV.Service]
DisplayName    = %SampleAVServiceName%
Description    = %SampleAVServiceDescription%
ServiceType    = 1       ; SERVICE_KERNEL_DRIVER
StartType      = 0       ; SERVICE_BOOT_START
ErrorControl   = 3       ; SERVICE_ERROR_CRITICAL
LoadOrderGroup = “Early-Launch”
```

由于 AM 驱动程序不拥有任何设备，因此有必要为旧安装 AM 驱动程序，因此驱动程序将仅作为服务添加到注册表。 （如果作为常规的即插即用驱动程序安装 AM 驱动程序，则它将添加到注册表的枚举部分，因此将 PDO 引用，这将导致不需要的行为时卸载该驱动程序。）

此外需要包括[SignatureAttributes 部分](inf-signatureattributes-section.md)ELAM 驱动程序的 INF 文件中。 

## <a name="backup-driver-installation"></a>备份驱动程序安装

若要 ELAM 驱动程序无意中损坏的情况下提供恢复机制，ELAM 安装程序会将驱动程序的副本也安装在备份位置。 这样，WinRE 检索干净副本和恢复安装。

安装程序读取从备份文件位置**BackupPath**密钥存储在

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

然后，安装程序会将备份的副本放入 regkey 中指定的文件夹。

## <a name="am-driver-initialization"></a>将驱动程序初始化


Windows 启动整个加载程序 Winload，加载所有引导启动驱动程序和其依赖的 Dll，到之前提交给 Windows 内核内存。 引导启动驱动程序表示在初始化磁盘堆栈之前进行初始化所需的设备驱动程序。 这些驱动程序包括其他人、 磁盘堆栈和卷管理器和文件系统驱动程序和操作系统设备的总线驱动程序。

## <a name="am-driver-callback-interface"></a>将驱动程序回调接口


ELAM 驱动程序使用回调来提供即插即用其描述为每个引导启动驱动程序和相关的 DLL，管理器，它可以对每个启动映像作为已知良好的二进制文件、 已知错误的二进制或未知的二进制文件进行分类。

默认操作系统策略是未初始化的已知错误的驱动程序和 Dll。 可以配置策略，并通过 Winload 认为启动证明的一部分。

即插即用使用策略和 AM 驱动程序提供的分类来确定是否初始化每个启动映像。

### <a name="registry-callbacks"></a>注册表回调

早期启动驱动程序可以使用注册表或启动驱动程序回调来监视和验证作为输入用于每个引导启动驱动程序的配置数据。 配置数据存储在系统注册表配置单元，它由 Winload 加载并在启动驱动程序初始化时。 这些回调有效 ELAM 驱动程序的生存期，卸载该驱动程序时将取消注册。 有关详细信息，请参阅：

* [**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921)
* [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)
* [**CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)

### <a name="boot-driver-callbacks"></a>启动驱动程序回调

使用[ **IoRegisterBootDriverCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439379)并[ **IoUnRegisterBootDriverCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh439394)注册和注销[ *BOOT_DRIVER_CALLBACK_FUNCTION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-boot_driver_callback_function)。

此回调提供了从 Windows 到 ELAM 驱动程序，包括所有引导启动驱动程序都已都初始化，回调功能将无法再正常运行时的状态更新。

### <a name="callback-type"></a>回调类型

[ **BDCB_CALLBACK_TYPE 枚举**](https://msdn.microsoft.com/library/windows/hardware/hh406352)介绍两种类型的回调：

-   为提供的 ELAM 驱动程序 (BdCbStatusUpdate) 的状态更新的回调
-   回调 AM 驱动程序用来对引导启动驱动程序和依赖 Dll 初始化其映像 (BdCbInitializeImage) 之前进行分类

两个回调类型具有唯一的上下文结构，并提供特定于回调的其他信息。

状态更新回调的上下文结构包含描述 Windows 标注的单个枚举的类型。

初始化映像回调的上下文结构是更复杂，其中包含每个加载的图像的哈希和证书信息。 此外，该结构包含 AM 驱动程序在其中存储驱动程序的分类类型是一个 output 参数的字段。

从状态更新回调返回的错误被视为致命错误，因而会导致检查系统错误。 这提供 ELAM 驱动程序的功能，以指示何时达到之外 AM 策略状态。 例如，如果 AM 运行时驱动程序未加载并初始化，早期启动驱动程序可能会失败准备卸载回调，以防止 Windows 进入的状态而无需 AM 加载驱动程序。

图像将被视为未知时从初始化映像回调返回错误。 未知的驱动程序将初始化或具有其跳过初始化基于操作系统策略。

## <a name="malware-signatures"></a>恶意软件签名

恶意软件签名数据由 AM ISV，但应包括，至少也允许列表中的驱动程序哈希值。 在新"早期启动驱动程序"配置单元下加载的 Winload 的 HKLM 注册表中存储的签名数据。 每个 AM 驱动程序有一个唯一键用来存储其签名二进制大型对象 (BLOB)。 注册表路径和密钥格式：

```cpp
HKLM\ELAM\<VendorName>\
```

项中，供应商可以自由地定义和使用的任何值。
有三个定义的二进制 blob 值的标准引导测量和供应商可能会使用每个：

-   测量
-   策略
-   Config

ELAM hive 后卸载其使用通过早期启动反恶意软件的性能。 如果用户模式服务想要更新的签名数据，它应装载的文件位置中的 hive 文件\\Windows\\System32\\config\\ELAM。 例如，无法生成 UUID、 将其转换为字符串，并将其用作要装入该配置单元的唯一键。
这些数据 Blob 的存储和检索格式应由 ISV，但必须签名的签名数据，以便 AM 驱动程序可以验证数据的完整性。

**验证恶意软件签名**

每个 AM ISV 最保留用于验证的恶意软件签名数据的完整性的方法。 [CNG 加密基元函数](https://msdn.microsoft.com/library/windows/desktop/aa833130)可协助验证数字签名和证书上的恶意软件签名数据。

**恶意软件签名失败**

如果 ELAM 驱动程序检查的签名数据，以及检查完整性失败，或者如果没有签名的数据，仍会成功的 ELAM 驱动程序初始化。 在这种情况下，对于每个引导驱动程序 ELAM 驱动程序必须返回"未知"的每次初始化回调。 此外，ELAM 驱动程序应将此信息传递到运行时 AM 组件上启动后。

## <a name="unloading-the-am-driver"></a>卸载 AM 驱动程序


BdCbStatusPrepareForUnload 回调 StatusType 时，这是到上午驱动程序指示所有启动驱动程序都已初始化，AM 驱动程序应准备卸载。 卸载前倒带，开机初期启动 AM 驱动程序需要取消注册其回调。 取消注册回调; 期间不会发生相反，它具有发生这种情况在 DriverUnload 函数中，可在 DriverEntry 期间指定驱动程序。

若要保持在恶意软件防护的连续性并确保正确切换，应在早期启动 AM 的驱动程序正在卸载之前启动 AM 运行时引擎。 这意味着，运行时 AM 引擎应验证早期启动 AM 驱动程序的启动驱动程序。

## <a name="performance"></a>性能


该驱动程序必须满足下表中定义的性能要求：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>方案</p></td>
<td align="left"><p>Start Time</p></td>
<td align="left"><p>结束时间</p></td>
<td align="left"><p>上限</p></td>
</tr>
<tr class="even">
<td align="left"><p>使其能够初始化之前，请评估加载的启动关键驱动程序。 这还包括状态更新回调。</p></td>
<td align="left"><p>内核回拨到反恶意软件驱动程序来评估加载的启动关键驱动程序。</p></td>
<td align="left"><p>反恶意软件驱动程序将返回评估结果。</p></td>
<td align="left"><p>0.5ms</p></td>
</tr>
<tr class="odd">
<td align="left"><p>评估所有已加载的启动关键驱动程序</p></td>
<td align="left"><p>内核调用返回到反恶意软件驱动程序来评估第一个加载的启动关键驱动程序。</p></td>
<td align="left"><p>反恶意软件驱动程序将返回最后一个启动关键驱动程序的计算结果。</p></td>
<td align="left"><p>50 毫秒</p></td>
</tr>
<tr class="even">
<td align="left"><p>内存占用 (驱动程序 + 配置内存中的数据)</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>128kB</p></td>
</tr>
</tbody>
</table>

 

## <a name="initializing-drivers"></a>初始化驱动程序


一旦启动驱动程序评估 ELAM 驱动程序，内核使用返回的 ELAM 的分类来确定是否要初始化的驱动程序。 此决定根据策略来确定和此处存储在注册表的以下位置：

```cpp
HKLM\System\CurrentControlSet\Control\EarlyLaunch\DriverLoadPolicy
```

这可以是通过组策略配置已加入域的客户端上。 反恶意软件解决方案可能想要将此功能提供给最终用户在未托管方案中。 DriverLoadPolicy 定义以下值：
```cpp
PNP_INITIALIZE_DRIVERS_DEFAULT 0x0  (initializes known Good drivers only)
PNP_INITIALIZE_UNKNOWN_DRIVERS 0x1  
PNP_INITIALIZE_BAD_CRITICAL_DRIVERS 0x3 (this is the default setting)
PNP_INITIALIZE_BAD_DRIVERS 0x7
```

## <a name="boot-failures"></a>启动失败


如果由于初始化策略，启动驱动程序将跳过，内核会继续尝试初始化列表中的下一步启动驱动程序。 此过程将继续，直到所有在初始化驱动程序，或启动失败，因为已跳过启动驱动程序的启动关键。 如果启动磁盘堆栈后，将发生崩溃，则没有故障转储，，它包含的原因，或者在发生崩溃，以包括有关缺少的驱动程序信息的一些信息。 这可在 WinRE 中来确定失败的原因并尝试修正。

## <a name="elam-and-measured-boot"></a>ELAM 和标准的引导


如果 ELAM 驱动程序检测到违反策略的情况 (例如，rootkit)，则应立即调用[ **Tbsi_Revoke_Attestation** ](https://docs.microsoft.com/windows/desktop/api/tbs/nf-tbs-tbsi_revoke_attestation)要使之无效 PCRs，表明系统已处于良好状态。 如果问题与标准引导，例如在系统上没有 TPM，该函数将返回错误。

**Tbsi_Revoke_Attestation**可从内核模式下调用。 它通过未指定的值来扩展 PCR [12] 并递增在 TPM 中的事件计数器。 这两种操作是有必要，因此以从转发此处创建的所有引号破坏信任。 因此，标准引导日志将不反映其余部分的时间的 TPM 已启动，TPM 的当前状态和远程系统将不能为窗体中的系统的安全状态的信任。
