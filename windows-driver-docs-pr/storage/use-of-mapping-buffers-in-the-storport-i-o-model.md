---
title: 在 Storport I/O 模型中使用映射缓冲区
description: 在 Storport I/O 模型中使用映射缓冲区
ms.assetid: cd22ec31-ff4d-42d4-a47d-7b8bd85804be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9c9399916c0c89ac76be0fabae4a367b88b7567
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386804"
---
# <a name="use-of-mapping-buffers-in-the-storport-io-model"></a>在 Storport I/O 模型中使用映射缓冲区


## <span id="ddk_use_of_mapping_buffers_in_the_storport_i_o_model_kg"></span><span id="DDK_USE_OF_MAPPING_BUFFERS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI 端口 I/O 模型，微型端口驱动程序可能需要端口驱动程序分配和映射的 SRB I/O 缓冲区的系统虚拟内存。 微型端口驱动程序配置的端口驱动程序来设置映射 I/O 缓冲区**MapBuffers**的成员[**端口\_配置\_信息 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)结构**TRUE**。

如果端口驱动程序配置了**MapBuffers**设置为**TRUE**，则**DataBuffer**的微型端口驱动程序将收到每个 SRB 成员将包含虚拟系统I/O 缓冲区的地址。 此地址是在系统中的所有进程的地址空间中有效。 此外，微型端口驱动程序将不收取直接访问 I/O 的缓冲区。

另一方面，如果微型端口驱动程序设置**MapBuffers**到**FALSE**， **DataBuffer**将包含属于一个特殊进程，不是一个虚拟地址微型端口驱动程序运行所在的上下文中一定有效。 因此，微型端口驱动程序将无法再访问的内存区域**DataBuffer**点。

Storport I/O 模型，微型端口驱动程序所需支持基于 DMA 的 I/O。 当使用 DMA 时，应通过系统范围内的虚拟地址间接访问 SRB 的 I/O 缓冲区的微型端口驱动程序不需要。 在视图中，与此 Storport I/O 模型定义一组不同的值**MapBuffers**的成员[**端口\_配置\_信息 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)).

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STOR_MAP_NO_BUFFERS</p></td>
<td align="left"><p>Storport 驱动程序没有为任何类型的 SRB 映射数据缓冲区。 因此，其微型端口驱动程序必须<em>不</em>直接访问指向的数据<strong>DataBuffer</strong>中收到的 Srb 的任何成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STOR_MAP_ALL_BUFFERS</p></td>
<td align="left"><p>目前尚未实现此功能。 如果<strong>MapBuffers</strong>成员分配此值，Storport 驱动程序，就好像它是 STOR_MAP_NON_READ_WRITE_BUFFERS 将其解释。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOR_MAP_NON_READ_WRITE_BUFFERS</p></td>
<td align="left"><p>Storport 驱动程序映射的数据缓冲区的请求，提供它不是数据传输 （读取和写入） 请求。 同样，微型端口驱动程序可以访问 SRB 中的数据，前提是 SRB 不属于读取或写入请求。</p></td>
</tr>
</tbody>
</table>

 

 

 




