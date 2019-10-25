---
title: 在 Storport I/O 模型中使用映射缓冲区
description: 在 Storport I/O 模型中使用映射缓冲区
ms.assetid: cd22ec31-ff4d-42d4-a47d-7b8bd85804be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9b2522ca2895b24f9ff8d42310980f8586594a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844438"
---
# <a name="use-of-mapping-buffers-in-the-storport-io-model"></a>在 Storport I/O 模型中使用映射缓冲区


## <span id="ddk_use_of_mapping_buffers_in_the_storport_i_o_model_kg"></span><span id="DDK_USE_OF_MAPPING_BUFFERS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


在 SCSI 端口 i/o 模型中，微型端口驱动程序可以要求端口驱动程序为 SRB i/o 缓冲区分配和映射系统虚拟内存。 微型端口驱动程序通过将[**端口\_配置\_信息（SCSI）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)结构中的**MapBuffers**成员设置为**TRUE**，将端口驱动程序配置为映射 i/o 缓冲区。

如果将**MapBuffers**设置为 TRUE，则端口驱动程序将设置为**TRUE**，微型端口驱动程序接收的每个 SRB 的**DataBuffer**成员将包含 i/o 缓冲区的系统虚拟地址。 此地址在系统中所有进程的地址空间中都有效。 此外，微型端口驱动程序将可以自由地直接访问 i/o 缓冲区。

另一方面，如果微型端口驱动程序将**MapBuffers**设置为**FALSE**，则**DataBuffer**将包含属于特定进程的虚拟地址，该进程在微型端口驱动程序运行的上下文中不一定有效。 因此，微型端口驱动程序将无法访问**DataBuffer**点的内存区域。

在 Storport i/o 模型中，需要微型端口驱动程序以支持基于 DMA 的 i/o。 使用 DMA 时，无需微端口驱动程序通过系统范围的虚拟地址间接访问 SRB 的 i/o 缓冲区。 在视图中，Storport i/o 模型为[**端口\_配置\_信息（Storport）** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))的**MapBuffers**成员定义一组不同的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STOR_MAP_NO_BUFFERS</p></td>
<td align="left"><p>Storport 驱动程序不会为任何类型的 SRB 映射数据缓冲区。 因此，其微型端口驱动程序<em>不</em>能直接访问其接收的任何 SRBs 中<strong>DataBuffer</strong>成员指向的数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STOR_MAP_ALL_BUFFERS</p></td>
<td align="left"><p>当前未实现此功能。 如果为<strong>MapBuffers</strong>成员分配了此值，则 Storport 驱动程序会将其解释为 STOR_MAP_NON_READ_WRITE_BUFFERS。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOR_MAP_NON_READ_WRITE_BUFFERS</p></td>
<td align="left"><p>Storport 驱动程序映射请求的数据缓冲区，前提是它不是数据传输（读取和写入）请求。 同样，小型端口驱动程序可以访问 SRB 中的数据，前提是 SRB 不属于读取或写入请求。</p></td>
</tr>
</tbody>
</table>

 

 

 




