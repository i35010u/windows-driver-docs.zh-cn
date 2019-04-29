---
title: OID_WWAN_PIN_EX2
description: OID_WWAN_PIN_EX2 访问 UICC 线性固定或循环文件，该结构类型是 WwanUiccFileStructureCyclic 或 WwanUiccFileStructureLinear。
ms.assetid: F5D0A1B8-4D7E-469A-B738-2965D254868E
ms.date: 04/10/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_PIN_EX2 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 126f8a38903e477bffe60b07086d038050518124
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354577"
---
# <a name="oidwwanpinex2"></a>OID_WWAN_PIN_EX2

OID_WWAN_PIN_EX2 设置或返回与个人标识号 (Pin) 相关的扩展的信息。 OID_WWAN_PIN_EX2 是类似于[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)，但将其扩展到支持多应用 UICC 卡。

查询有效负载包含[ **NDIS_WWAN_PIN_APP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)正被查询的结构，它指定目标应用程序 ID 的 PIN。 微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状态通知包含[ **NDIS_WWAN_PIN_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)介绍 PIN 进行应用程序的结构。 

设置有效负载包含[ **NDIS_WWAN_SET_PIN_EX2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)结构，它指定要执行的应用程序的固定操作。 微型端口驱动程序必须设置异步处理请求，最初在更高版本发送之前对原始请求返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状态通知包含[ **NDIS_WWAN_PIN_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)结构，它描述应用程序的固定状态。

## <a name="remarks"></a>备注

仅单个验证能够 UICCs 都受支持。 支持多 verification 的 UICCs 支持多个应用程序不支持固定的。 一个应用程序 PIN (PIN1) 分配给所有 ADFs/DFs 和 UICC 上的文件。 但是，每个应用程序可以指定为级别 2 用户验证要求，从而需要为每个访问命令的其他验证为本地固定 (PIN2)。 这种情况下是 OID_WWAN_PIN_EX2 的支持。

就像[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)，与 OID_WWAN_PIN_EX2 设备只报告一个插针一次。 如果启用了多个插针，并且启用报告多个插针，然后微型端口驱动程序必须报告 PIN1 第一次。 例如，如果启用 SIM 的 PIN1 启用 subsidy 锁报告，然后 subsidy 锁定 PIN 中应该报告的后续查询请求才通过将设置指定 PIN1 **PinSize**为零 (0)。 在这种情况下，Set 请求类似于查询并返回所引用的 PIN 的状态。 这完全对齐的行为的验证命令的节指定 11.1.9 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。

有关此 OID 的使用情况的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)

[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)

[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)

[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)
