---
title: ELAM 驱动程序要求
description: 驱动程序安装必须使用现有的工具进行联机和脱机安装，并通过典型的 INF 处理注册驱动程序。
ms.assetid: B00B4361-B531-4D28-A521-0F8B3B48CEA4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cfff0b6fa5eb5d67bbc9594ff4ed3b6e1dab465
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828819"
---
# <a name="elam-driver-requirements"></a>ELAM 驱动程序要求


驱动程序安装必须使用现有的工具进行联机和脱机安装，并通过典型的 INF 处理注册驱动程序。  有关 ELAM 驱动程序代码示例，请参阅以下内容： https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam 

## <a name="am-driver-installation"></a>AM 驱动程序安装


为了确保驱动程序安装兼容性，ELAM 驱动程序将自身作为启动启动驱动程序播发，这类似于所有其他启动启动驱动程序。 INF 将启动类型设置为 SERVICE_BOOT_START （0），这表示驱动程序应由启动加载程序加载并在内核初始化期间初始化。 ELAM 驱动程序将其组播发为 "预先启动"。 此组中的驱动程序的早期启动行为将在 Windows 中实现，如下一节中所述。

下面是 ELAM 驱动程序 INF 的驱动程序安装部分的示例。

```cpp
[SampleAV.Service]
DisplayName    = %SampleAVServiceName%
Description    = %SampleAVServiceDescription%
ServiceType    = 1       ; SERVICE_KERNEL_DRIVER
StartType      = 0       ; SERVICE_BOOT_START
ErrorControl   = 3       ; SERVICE_ERROR_CRITICAL
LoadOrderGroup = “Early-Launch”
```

由于 AM 驱动程序不拥有任何设备，因此需要将 AM 驱动程序安装为旧式驱动程序，以便仅将驱动程序作为服务添加到注册表中。 （如果将 AM 驱动程序作为普通 PNP 驱动程序安装，则会将其添加到注册表的 enum 部分，因此将具有 PDO 引用，这将导致卸载驱动程序时出现不需要的行为。）

还需要在 INF 文件中包含 ELAM 驱动程序的[SignatureAttributes 部分](inf-signatureattributes-section.md)。 

## <a name="backup-driver-installation"></a>备份驱动程序安装

若要在 ELAM 驱动程序无意中损坏的情况下提供一种恢复机制，ELAM 安装程序还会在备份位置安装该驱动程序的副本。 这将允许 WinRE 检索干净副本并恢复安装。

安装程序从存储在中的**BackupPath**密钥读取备份文件位置

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

然后，安装程序将备份副本放置在 regkey 中指定的文件夹中。

## <a name="am-driver-initialization"></a>AM 驱动程序初始化


Windows 启动加载程序 Winload.exe 将所有启动驱动程序及其依赖 Dll 加载到 Windows 内核之前，会将其加载到内存中。 引导启动驱动程序表示在初始化磁盘堆栈之前需要初始化的设备驱动程序。 这些驱动程序包括磁盘堆栈和卷管理器以及操作系统设备的文件系统驱动程序和总线驱动程序。

## <a name="am-driver-callback-interface"></a>AM 驱动程序回调接口


ELAM 驱动程序使用回调为 PnP 管理器提供每个启动启动驱动程序和依赖 DLL 的说明，并可以将每个启动映像分类为已知良好的二进制文件、已知错误的二进制文件或未知的二进制文件。

默认操作系统策略不能初始化已知的坏驱动程序和 Dll。 可以配置策略，并由 Winload.exe 作为启动证明的一部分来度量。

PnP 使用策略和 AM 驱动程序提供的分类来决定是否初始化每个启动映像。

### <a name="registry-callbacks"></a>注册表回调

早期启动驱动程序可以使用注册表或启动驱动程序回调来监视和验证用作每个启动启动驱动程序的输入的配置数据。 配置数据存储在系统注册表配置单元中，它由 Winload.exe 加载，在启动驱动程序初始化时可用。

> [!NOTE]
> 在系统启动之前，对 ELAM 注册表配置单元所做的任何更改都将被丢弃。
> 因此，ELAM 驱动程序应使用 Windows 的标准事件跟踪（ETW）日志记录，而不是写入注册表。

这些回调在 ELAM 驱动程序的生存期内有效，并且在卸载驱动程序时将被注销。 有关详细信息，请参阅：

* [**CmRegisterCallbackEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)
* [**CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)
* [**CmUnRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)

### <a name="boot-driver-callbacks"></a>启动驱动程序回调

使用[**IoRegisterBootDriverCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterbootdrivercallback)和[**IoUnRegisterBootDriverCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iounregisterbootdrivercallback)注册和注销[*BOOT_DRIVER_CALLBACK_FUNCTION*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-boot_driver_callback_function)。

此回调提供从 Windows 到 ELAM 驱动程序的状态更新，包括所有启动启动驱动程序都已初始化并且回调功能不再正常工作。

### <a name="callback-type"></a>回调类型

[**BDCB_CALLBACK_TYPE 枚举**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ne-ntddk-_bdcb_callback_type)描述了两种类型的回调：

-   向 ELAM 驱动程序提供状态更新的回调（BdCbStatusUpdate）
-   AM 驱动程序使用的回调，用于在初始化启动驱动程序和依赖 Dll 之前对其映像进行分类（BdCbInitializeImage）

这两个回调类型具有唯一的上下文结构，它们提供特定于回调的附加信息。

状态更新回叫的上下文结构包含一个描述 Windows 标注的枚举类型。

用于初始化映像回调的上下文结构更复杂，其中包含每个加载的映像的哈希和证书信息。 该结构还包含一个字段，该字段是 AM 驱动程序为驱动程序存储分类类型的输出参数。

从状态更新回调返回的错误被视为错误，并导致系统 bug 检查。 这会提供 ELAM 驱动程序，用于指示何时到达 AM 策略以外的状态。 例如，如果未加载和初始化 AM 运行时驱动程序，则早期启动驱动程序可能会失败 "准备卸载" 回调，以防止 Windows 进入未加载 AM 驱动程序的状态。

从初始化图像回调返回错误时，图像被视为未知。 未知的驱动程序已初始化，或者根据 OS 策略跳过了其初始化。

## <a name="malware-signatures"></a>恶意软件签名

恶意软件签名数据由 AM ISV 决定，但至少应包含一个批准的驱动程序哈希列表。 签名数据存储在 Winload.exe 所加载的 HKLM 下新的 "早期启动驱动程序" 配置单元中。 每个 AM 驱动程序都有一个唯一键，用于存储其签名二进制大型对象（BLOB）。 注册表路径和密钥的格式如下：

```cpp
HKLM\ELAM\<VendorName>\
```

在该密钥中，供应商可以自由定义和使用任何值。
有三个已定义的二进制 blob 值，这些值通过测量的启动进行度量，供应商可以使用每个值：

-   测量
-   策略
-   Config

ELAM 配置单元在使用后将通过早期启动反恶意软件以提高性能。 如果用户模式服务要更新签名数据，则应将该配置文件的文件位置 \\Windows\\System32\\config\\ELAM。 例如，可以生成一个 UUID，将其转换为字符串，并将其用作装载 hive 的唯一键。
这些数据 Blob 的存储和检索格式将留给 ISV，但必须对签名数据进行签名，以便 AM 驱动程序可以验证数据的完整性。

**验证恶意软件签名**

验证恶意软件签名数据完整性的方法留给每个 AM ISV。 [CNG 加密基元函数](https://docs.microsoft.com/windows/desktop/SecCNG/cng-cryptographic-primitive-functions)可用于帮助验证恶意软件签名数据上的数字签名和证书。

**恶意软件签名失败**

如果 ELAM 驱动程序检查签名数据的完整性并且该检查失败，或者如果没有签名数据，则 ELAM 驱动程序的初始化仍会成功。 在这种情况下，对于每个启动驱动程序，ELAM 驱动程序必须针对每个初始化回调返回 "unknown"。 此外，在启动时，ELAM 驱动程序应将此信息传递到运行时 AM 组件。

## <a name="unloading-the-am-driver"></a>卸载 AM 驱动程序


当回调 StatusType 为 BdCbStatusPrepareForUnload 时，这是对 AM 驱动程序的指示，表示所有启动驱动程序都已初始化，AM 驱动程序应准备好卸载。 卸载之前，早期启动 AM 驱动程序需要取消注册其回调。 在回调过程中不能取消注册;相反，它必须在 DriverUnload 函数中发生，驱动程序可以在 DriverEntry 期间指定该函数。

为了保持恶意软件防护的连续性并确保正确地进行切换，应在卸载早期启动 AM 驱动程序之前启动运行时 AM 引擎。 这意味着，运行时 AM 引擎应是由早期启动 AM 驱动程序验证的启动驱动程序。

## <a name="performance"></a>性能


驱动程序必须满足下表中定义的性能要求：

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
<td align="left"><p>评估已加载的启动关键驱动程序，然后允许它初始化。 这还包括状态更新回调。</p></td>
<td align="left"><p>内核回叫反恶意软件驱动程序以评估加载的启动关键驱动程序。</p></td>
<td align="left"><p>反恶意软件驱动程序返回计算结果。</p></td>
<td align="left"><p>0.5 毫秒</p></td>
</tr>
<tr class="odd">
<td align="left"><p>评估所有已加载的启动关键驱动程序</p></td>
<td align="left"><p>内核回叫反恶意软件驱动程序，以评估首次加载的启动关键驱动程序。</p></td>
<td align="left"><p>反恶意软件驱动程序返回上一次启动关键驱动程序的评估结果。</p></td>
<td align="left"><p>50 ms</p></td>
</tr>
<tr class="even">
<td align="left"><p>占用空间（驱动程序 + 内存中的配置数据）</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>128kB</p></td>
</tr>
</tbody>
</table>

 

## <a name="initializing-drivers"></a>初始化驱动程序


一旦 ELAM 驱动程序计算启动驱动程序，内核就会使用 ELAM 返回的分类来决定是否初始化驱动程序。 此决定由策略决定，存储在注册表中的以下位置：

```cpp
HKLM\System\CurrentControlSet\Control\EarlyLaunch\DriverLoadPolicy
```

这可以通过已加入域的客户端上的组策略进行配置。 反恶意软件解决方案可能需要在未托管方案中向最终用户公开此功能。 为 DriverLoadPolicy 定义了以下值：
```cpp
PNP_INITIALIZE_DRIVERS_DEFAULT 0x0  (initializes known Good drivers only)
PNP_INITIALIZE_UNKNOWN_DRIVERS 0x1  
PNP_INITIALIZE_BAD_CRITICAL_DRIVERS 0x3 (this is the default setting)
PNP_INITIALIZE_BAD_DRIVERS 0x7
```

## <a name="boot-failures"></a>启动故障


如果由于初始化策略而跳过启动驱动程序，内核将继续尝试初始化列表中的下一个启动驱动程序。 这会持续到驱动程序全部初始化，或启动失败，因为跳过的启动驱动程序对启动至关重要。 如果在磁盘堆栈启动后发生崩溃，则会出现故障转储，并包含有关原因或崩溃的一些信息，以包括有关缺少的驱动程序的信息。 可在 WinRE 中使用此项来确定失败的原因并尝试修正。

## <a name="elam-and-measured-boot"></a>ELAM 和度量启动


如果 ELAM 驱动程序检测到策略冲突（例如 rootkit），则它应立即调用[**Tbsi_Revoke_Attestation**](https://docs.microsoft.com/windows/desktop/api/tbs/nf-tbs-tbsi_revoke_attestation) ，使指示系统处于良好状态的 PCRs 失效。 如果度量启动有问题（例如系统上没有 TPM），该函数将返回错误。

可从内核模式调用**Tbsi_Revoke_Attestation** 。 它通过未指定的值扩展 PCR [12]，并递增 TPM 中的事件计数器。 这两个操作都是必需的，因此，从此处开始创建的所有引号中的信任会断开。 因此，经过度量的启动日志不会反映 tpm 的当前状态，这是 TPM 通电后的剩余时间，远程系统将无法在系统的安全状态下形成信任。
