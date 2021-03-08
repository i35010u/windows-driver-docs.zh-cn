---
title: ESIM 的 MB 固件升级
description: ESIM 的 MB 固件升级
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: c4413300fbf53415f80a8632bb1711ab980f64b4
ms.sourcegitcommit: afc34ee2a8cafd038e9da86e240f9c7fceb2ecff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102450704"
---
# <a name="firmware-upgrade-for-esim"></a>ESIM 固件升级

## <a name="overview"></a>概述
本文档介绍了支持 eSIM 设备固件更新的 Windows OS 更改。 

Windows 更新 (WU) 是用于固件修补程序的模型。 在此模型中，eSIM 设备供应商创建一个 UMDF 驱动程序，并将其添加到 WU 包以及固件修补程序。 包将发布到 WU，并将下载 & 安装在包含卡供应商 eSIM 设备的 Windows 设备上。 安装该卡供应商的驱动程序后，将使用智能卡 WinRT API 写入固件修补程序。 Microsoft 通过为 eSIM 的 ISO 接口提供 UMDF 驱动程序并通过现有的智能卡 WinRT API 将其作为智能卡进行公开，从而实现此功能。

调制解调器 ISO 接口的限制为255字节的限制，因为 max 应用程序协议数据单元 (APDU) 大小，因此对于完整固件 OS 更新 (TRACE.DAT.TRC/PBL 映像) 的速度太慢。 对于完整固件 OS 更新，Microsoft 提供了一个单独的智能卡 UMDF 驱动程序，该驱动程序使用 eSIM 的 SPB 接口作为传输。

本部分使用以下首字母缩写：
- **ACPI：** 高级配置和电源接口
- **APDU：** 应用程序协议数据单元
- **ATR：** 重置答案  
- **eUICC：**  嵌入式通用集成电路卡
- **FW：** 固件
- **HCP：** 主机控制器协议
- **HWID：** 硬件 ID
- **ISO：** 国际标准化组织
- **MF：** Master 文件
- **MSFT：** 微软
- **OEM：** 原始设备制造商
- **PBL：** 主引导加载
- **RPC：** 远程过程调用
- **ScardSvr：** 适用于 Windows 服务的智能卡
- **放弃 WinRT：** 智能卡 Windows 运行时
- **SC DDI：** 智能卡 DDI
- **sHDLC：** 简化的高级数据链接控制
- **SPB：** 简单外围总线
- **SPI：** 串行外围设备接口
- **Trace.dat.trc：** 防篡改芯片
- **WwanSvc：** WWAN 服务

### <a name="high-level-design-for-firmware-patch-update"></a>固件修补程序更新的高级设计
![固件修补程序更新的高级设计](images\mb-fw-upgrade-esim-high-level-design.png "固件修补程序更新的高级设计")

### <a name="high-level-design-for-firmware-os-update"></a>固件 OS 更新的高级设计
![固件 OS 更新的高级设计](images\mb-fw-upgrade-esim-high-level-os-update.png "固件 OS 更新的高级设计")

## <a name="firmware-upgrade-architecture"></a>固件升级体系结构

![ESIM 块示意图升级固件](images\mb-fw-upgrade-esim-block-diag.png "ESIM 块示意图升级固件")

对于 Windows 10，版本1703：卡供应商将通过 ISO 接口在 Apdu 上传送固件更新。 为 Windows 10 版本1709的时间范围规划通过 SPI 接口 (PBL HCP) 上的完整映像更新。 

当 WWAN 服务检测到基于 ATR 信息的 eSIM 时，由 WWAN 服务加载 ISO UMDF 驱动程序。 ISO UMDF 驱动程序使用 WWAN 服务的低级 UICC 访问 RPC，将 Apdu 发送到 eUICC。 

基于 eSIM 卡的 ACPI 条目中的硬件 ID，PnP 加载 SPI UMDF 驱动程序。 SPI UMDF 驱动程序通过 SPB IOCTL 接口将 sHDLC 帧发送到卡上的 TRACE.DAT.TRC。 

在上层，这两个驱动程序将实现智能卡 DDI，这为与智能卡交互提供低级别访问权限。 这会通过智能卡 WinRT API 将 eSIM 的 ISO 和 SPI 接口公开为智能卡。

在可用 eSIM 的 SPI 接口的设备中，Oem 应将 Microsoft UICC SPI 驱动程序 HWID 作为硬件兼容 ID 添加到 ACPI 表中。 Microsoft UICC SPI 驱动程序的 HWID 是 ACPI\MSFTUICCSPB。

### <a name="umdf-drivers"></a>UMDF 驱动程序

UMDF 驱动程序将实现以下智能卡 IOCTLs：

|使用情况|DDI|
|---|---|
|智能卡状态|IOCTL_SMARTCARD_GET_STATE<BR>IOCTL_SMARTCARD_IS_ABSENT<BR>IOCTL_SMARTCARD_IS_PRESENT<BR>IOCTL_SMARTCARD_POWER|
|智能卡属性|IOCTL_SMARTCARD_GET_ATTRIBUTE<BR>IOCTL_SMARTCARD_SET_ATTRIBUTE|
|智能卡通信|IOCTL_SMARTCARD_SET_PROTOCOL<br>IOCTL_SMARTCARD_TRANSMIT|

#### <a name="requirements-for-smart-card-devices"></a>智能卡设备的要求

定义以下设备属性：

|定义|名称|类型|FormatID|Value|
|---|--- |--- |---     |---  |
|设备接口 guid|InterfaceClassGuid--PKEY_Devices_InterfaceClassGuid|Guid--VT_CLSID|{026E516E-B814-414B-83CD-856D6FEF4822}，4，DEVPROP_TYPE_GUID|{DEEBE6AD-9E01-47E2-A3B2-A66AA2C036C9}|
|ReaderKind| ReaderKind--PKEY_Devices_SmartCards_ReaderKind|字节--VT_UI1 (应为 INT16 Bug 9550228) |{D6B5B883-18BD-4B4D-B2EC-9E38AFFEDA82}、2 DEVPROP_TYPE_BYTE |SmartCardReaderKind_Uicc|
|ReaderName|DEVPKEY_Device_ReaderName (0xD6B5B883、0x18BD、0x4B4D、0xB2、0xEC、0x9E、0x38、0xAF、0xFE、0xDA、0x82、0x03) |String--variant 的 VT_LPWSTR (： VT_BSTR) |{D6B5B883-18BD-4B4D-B2EC-9E38AFFEDA82}，3，DEVPROP_TYPE_STRING|CustomName|
|AppAccessRestrictionsFlags| ReaderKind--PKEY_Devices_SmartCards_AppAccessRestrictionsFlags| 字节--VT_UI1|{D6B5B883-18BD-4B4D-B2EC-9E38AFFEDA82}，4，DEVPROP_TYPE_BYTE|PrivilegedAppOnly (1) |

ISO UMDF 驱动程序在智能卡读卡器 devnode 上设置更多自定义开发属性：

| 定义  |名称|类型|FormatID|Value|
|---|--- |--- |---     |---  |
|RadioName|DEVPKEY_MbbDevice_RadioName|： DEVPROP_TYPE_GUID |{41e061f2-9999-4b33-bf42-f950cbfd5f2e}，1，DEVPROP_TYPE_GUID |RadioInterfaceGuid|
|SlotId|DEVPKEY_MbbDevice_SlotId|DEVPROP_TYPE_UINT32|{c4c66992-3bcc-4f96-9a85-bd807235fbe1}、2 DEVPROP_TYPE_UINT32|SlotId|
|IsEmbedded|DEVPKEY_MbbDevice_IsEmbedded|DEVPROP_TYPE_BOOLEAN|{7d08a710-b448-4148-8049-0aa12e5fd2dd}，3，DEVPROP_TYPE_BOOLEAN|IsEmbedded|

这些属性用于唯一命名智能卡读卡器，并识别连接到正确的 eSIM 卡的读卡器。 例如： IsEmbedded = True 和 SlotId = 1。

![UICC ISO SC Driver DevNode 的其他自定义属性](images\mb-fw-upgrade-esim-Additional-Custom-Properties-for-UICCISOSCDriver-DevNode.png "UICC ISO SC Driver DevNode 的其他自定义属性")

TRACE.DAT.TRC 映像更新代理需要具有允许访问智能卡 WinRT API 的 sharedUserCertificates 功能。 SharedUserCertificates 功能是一种受限功能，只提供给具有特定凭据的企业。 授予访问权限后，应用可通过智能卡 API 连接到设备上的 TRACE.DAT.TRC，并将命令发送到该卡。

预期固件修补程序是通过 Apdu 传输的。 由于智能卡 WinRT API 只公开传输 Apdu，而不公开通道管理功能（如打开/关闭），因此，UMDF 驱动程序将检查 Apdu，并查找按辅导命令。 如果驱动程序找到 "按辅导" 命令，则会将其解释为使用 Wwan RPC API 打开逻辑通道。 UMDF 驱动程序将始终验证辅助工具是否 allowlisted，否则将拒绝该请求。 由于 SC DDI 中没有关闭或断开连接 IOCTL，因此 UMDF 驱动程序无法知道传输何时结束以及何时结束逻辑通道。 若要防止逻辑通道泄露，UMDF 驱动程序会在打开逻辑通道时设置5分钟计时器，并在计时器过期时关闭通道。 5分钟的时间应足够长，因为固件更新预计最多可运行2.5 分钟。 如果 UMDF 驱动程序检测到新的 SELECT by 辅助命令，它将关闭先前打开的通道，并重置新逻辑通道的计时器。 请注意，5分钟超时值是从上次传输的 APDU 度量的。 换句话说，通过现有通道传输 APDU 会重置计时器。

若要防止针对随机 UICC 应用打开通道，ISO UMDF 驱动程序将允许更新所需的应用 Id，并将访问权限仅限于这些应用。 卡供应商可帮助识别应用 Id，OEM 会将 Id 添加为注册表项。 此外，智能卡中的 UICC 应用程序还应在固件上执行数字签名检查，以防止恶意应用发送数据。

##### <a name="cosa-setting"></a>COSA 设置
`CellCore/PerDevice/eSIM/FwUpdate/AllowedAppIdList`

在完整固件 OS 更新期间，不能访问涉及的 UICC 应用程序，这一点很重要。 若要实现此目的，TRACE.DAT.TRC 映像更新代理将发送一个特殊的 APDU，指示 eUICC 转入 TRACE.DAT.TRC/PBL 模式。 然后，TRACE.DAT.TRC 应用程序会要求调制解调器进入直通模式并重置该卡。 该卡将作为空 MF 启动。 完成更新后，将要求调制解调器再次重置该卡。 这一次，调制解调器和卡都将返回到正常模式。

## <a name="flow-diagrams"></a>流程图
### <a name="connect"></a>连接
![用于连接到 SC WinRT 的流程图](images\mb-fw-upgrade-esim-connect.png "连接")
### <a name="transmit-open-channel"></a>传输 (开放通道) 
![传输 (打开通道的流程图) ](images\mb-fw-upgrade-esim-transmit-open-channel.png "交易打开通道")
### <a name="transmit-send-apdu-and-close-channel"></a>传输 (发送 APDU 并结束通道) 
![传输 (发送 APDU 和结束通道) 的流程图 ](images\mb-fw-upgrade-esim-transmit-sendapdu-close-channel.png "传输发送 apdu & 关闭通道")
### <a name="get-atr"></a>获取 ATR
![Get ATR 的流程图](images\mb-fw-upgrade-esim-getatr.png "获取 ATR")
### <a name="pass-through-mode"></a>传递模式
![直通模式的流程图](images\mb-fw-upgrade-esim-passthru.png "传递")

## <a name="related"></a>相关内容 
[使用已发布的 DISM 预安装应用](/previous-versions/windows/it-pro/windows-8.1-and-8/dn387084(v=win.10)?redirectedfrom=MSDN)

[向桌面映像添加预安装的应用](/windows-hardware/customize/preinstall/preinstallable-apps-for-windows-10-desktop) 

[适用于移动设备的可预装应用](/windows-hardware/customize/preinstall/preinstallable-apps-for-window-10-for-phones)

[预安装任务](/windows-hardware/customize/preinstall/preinstall-tasks)



