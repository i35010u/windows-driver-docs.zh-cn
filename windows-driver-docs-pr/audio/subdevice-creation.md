---
title: 创建子设备
description: 创建子设备
ms.assetid: e4ba1209-adc6-48c3-9633-247e9e3849bc
keywords:
- 音频适配器 WDK，subdevices
- 适配器驱动程序 WDK 音频，subdevices
- subdevices WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b66c8b9d7c71316c78d3cfec59ab68780c68b36b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832352"
---
# <a name="subdevice-creation"></a>创建子设备


## <span id="subdevice_creation"></span><span id="SUBDEVICE_CREATION"></span>


术语 " *subdevice* " 用于描述下表中列出的四个组件的绑定。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Component</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口对象</p></td>
<td align="left"><p>公开微型端口驱动程序的 IMiniport<em>Xxx</em>接口的对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口对象</p></td>
<td align="left"><p>一个对象，该对象公开端口驱动程序的 IPort<em>Xxx</em>接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>资源列表对象</p></td>
<td align="left"><p>一个对象，它包含分配给 subdevice 的适配器驱动程序资源列表</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用字符串</p></td>
<td align="left"><p>添加到设备路径名称的名称，用于在创建筛选器时指定 subdevice</p></td>
</tr>
</tbody>
</table>

 

Subdevice 的 IMiniport*xxx*和 IPort*xxx*接口分别继承自基接口[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)和[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)。

PortCls 系统驱动程序不区分端口驱动程序和微型端口驱动程序。 它只需要一个对象（例如端口对象）以及一个可以处理系统生成的请求的接口。

同样，PortCls 不会直接纳入管理资源。 只需将请求处理程序（端口驱动程序）绑定到资源列表。 适配器驱动程序负责将端口、微型端口和资源列表对象绑定在一起。

下面的代码示例演示如何执行以下操作：

```cpp
  //
  // Instantiate the port by calling a function supplied by PortCls.
  //
  PPORT    port;
  NTSTATUS ntStatus = PcNewPort(&port, PortClassId);

  if (NT_SUCCESS(ntStatus))
  {
      PUNKNOWN miniport;
      //
      // Create the miniport object.
      //
      if (MiniportCreate)   // a function to create a proprietary miniport
      {
          ntStatus = MiniportCreate(&miniport,
                                    MiniportClassId, NULL, NonPagedPool);
      }
      else   // Ask PortCls for one of its built-in miniports.
      {
          ntStatus = PcNewMiniport((PMINIPORT*)&miniport,
                                   MiniportClassId);
      }

      if (NT_SUCCESS(ntStatus))
      {
          //
          // Bind the port, miniport, and resources.
          //
          ntStatus = port->Init(DeviceObject,
                                Irp, miniport, UnknownAdapter, ResourceList);
          if (NT_SUCCESS(ntStatus))
          {
              //
              // Hand the port driver and the reference
              // string to PortCls.
              //
              ntStatus = PcRegisterSubdevice(DeviceObject,
                                             Name, port);
          }

          //
          // We no longer need to reference the miniport driver.
          // Either the port driver now references it,
          // or binding failed and it should be deleted.
          //
          miniport->Release();
      }

      //
      // Release the reference that existed when PcNewPort() gave us
      // the pointer in the first place. This reference must be released
      // regardless of whether the binding of the port and miniport
      // drivers succeeded.
      //
      port->Release();
  }
```

有关上述代码示例中的 PortCls 函数调用的信息，请参阅[**PcNewPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)、 [**PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)和[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)。

 

 




