---
title: 自动文档送纸器命令
description: 自动文档送纸器命令
ms.date: 11/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: a136dbc09620c82e9dcfb7e49fae9e005f3f2df3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828709"
---
# <a name="automatic-document-feeder-commands"></a>自动文档送纸器命令

本部分中的命令适用于支持自动文档送纸器 (ADF) 的 microdrivers。 若要报告 microdriver 支持自动文档送纸器，请将 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构中的 **ADF** 成员设置为 1 (或者2（如果 ADF 在 CMD_INITIALIZE 命令期间有双面打印器) 。 这将导致 WIA 平板驱动程序为 ADF 控制添加所需的属性，并使用本部分中的命令。

## <a name="cmd_load_adf"></a>CMD_LOAD_ADF  

由 WIA 平板驱动程序调用以将页面加载到 ADF。 如果此命令不适用于设备，请返回 E_NOTIMPL。 对于自动馈送页面的设备，此命令是可选的。

## <a name="cmd_unload_adf"></a>CMD_UNLOAD_ADF  

由 WIA 平板驱动程序调用，以从 ADF 中卸载页面。 如果此命令不适用于设备，请返回 E_NOTIMPL。 对于自动 unfeeds 页面的设备，此命令是可选的。

## <a name="cmd_getadfavailable"></a>CMD_GETADFAVAILABLE  

由 WIA 平板驱动程序调用，用于确定 ADF 是否可供使用。 如果 ADF 可用，请返回 S_OK。 如果此命令不适用于设备，请返回 E_NOTIMPL。

## <a name="cmd_getadfhaspaper"></a>CMD_GETADFHASPAPER  

由 WIA 平板驱动程序调用以获取设备 ADF 的纸张状态。 将传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员设置为适当的状态值。  (查看可能状态值的 CMD_ADFGETSTATUS。 ) 

## <a name="cmd_getadfopen"></a>CMD_GETADFOPEN  

与 CMD_GETADFREADY 相同。 WIA 平板驱动程序当前未使用此命令。

## <a name="cmd_getadfstatus"></a>CMD_GETADFSTATUS  

由 WIA 平板驱动程序调用以获取附加到设备的 ADF 的状态。 将传递的 [**VAL**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)结构的 **lVal** 成员设置为适当的状态值。 可能的状态值如下所示。

| 状态 | 含义 |
|--|--|
| MCRO_ERROR_GENERAL_ERROR | 常规错误 |
| MCRO_ERROR_OFFLINE | ADF 或设备处于脱机状态 |
| MCRO_ERROR_PAPER_EMPTY | 他没有纸 |
| MCRO_ERROR_PAPER_JAM | ADF 出现卡纸 |
| MCRO_ERROR_PAPER_PROBLEM | ADF 出现纸张问题 |
| MCRO_ERROR_USER_INTERVENTION | 用户需要与设备交互 |
| MCRO_STATUS_OK | 没有要报告的错误 |

## <a name="cmd_getadfunloadready"></a>CMD_GETADFUNLOADREADY  

由 WIA 平板驱动程序调用，用于确定 ADF 是否已准备好卸载页面。 如果是这样，请返回 S_OK。 如果此命令不适用于设备，请返回 E_NOTIMPL。
