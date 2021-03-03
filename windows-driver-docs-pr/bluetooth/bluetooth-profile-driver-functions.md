---
title: 蓝牙配置文件驱动程序函数
description: 配置文件驱动程序支持的蓝牙功能列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6647d82d4aad75d02ca57376b7ac488ecd3a4c1
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101751938"
---
# <a name="bluetooth-profile-driver-functions"></a>蓝牙配置文件驱动程序函数

本部分包含蓝牙驱动程序堆栈支持的下列蓝牙功能的参考页。

[BluetoothSetLocalServiceInfo](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothsetlocalserviceinfo)

[BthAllocateBrb](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)

[BthFreeBrb](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_free_brb)

[BthInitializeBrb](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)

[BthReuseBrb](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_reuse_brb)

[IsBluetoothVersionAvailable](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_is_bluetooth_version_available)

[SdpAddAttributeToTree](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpaddattributetotree)

[SdpAppendNodeToContainerNode](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[SdpByteSwapUint64](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pbyteswapuint64)

[SdpByteSwapUint128](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pbyteswapuint128)

[SdpByteSwapUuid128](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pbyteswapuuid128)

[SdpConvertStreamToTree](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)

[SdpCreateNodeAlternative](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodealternative)

[SdpCreateNodeBoolean](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeboolean)

[SdpCreateNodeInt8](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint8)

[SdpCreateNodeInt16](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint16)

[SdpCreateNodeInt32](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint32)

[SdpCreateNodeInt64](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint64)

[SdpCreateNodeInt128](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint128)

[SdpCreateNodeNil](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodenil)

[SdpCreateNodeSequence](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodesequence)

[SdpCreateNodeString](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodestring)

[SdpCreateNodeTree](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodetree)

[SdpCreateNodeUInt8](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint8)

[SdpCreateNodeUInt16](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint16)

[SdpCreateNodeUInt32](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint32)

[SdpCreateNodeUInt64](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint64)

[SdpCreateNodeUInt128](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint128)

[SdpCreateNodeUrl](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeurl)

[SdpCreateNodeUUID16](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[SdpCreateNodeUUID32](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid32)

[SdpCreateNodeUUID128](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[SdpFindAttributeInTree](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfindattributeintree)

[SdpFreeTree](/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfreetree)

[SdpGetNextElement](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pgetnextelement)

[SdpRetrieveUint64](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pretrieveuint64)

[SdpRetrieveUuid128](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pretrieveuuid128)

[SdpValidateStream](/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pvalidatestream)

## <a name="see-also"></a>另请参阅

[L2CAP 客户端连接](creating-a-l2cap-client-connection-to-a-remote-device.md)

[SCO 客户端连接](creating-a-sco-client-connection-to-a-remote-device.md)
