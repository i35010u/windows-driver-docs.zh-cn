---
title: 创建子设备
description: 创建子设备
ms.assetid: e4ba1209-adc6-48c3-9633-247e9e3849bc
keywords:
- 音频适配器 WDK，子设备
- 适配器驱动程序 WDK 音频，子设备
- 子设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0171b629b3a5978cd90b72fd2f617e0f6f1697c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328603"
---
# <a name="subdevice-creation"></a>创建子设备


## <span id="subdevice_creation"></span><span id="SUBDEVICE_CREATION"></span>


术语*子*用来描述下表中列出的四个组件的绑定。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>微型端口对象</p></td>
<td align="left"><p>对象公开微型端口驱动程序的 IMiniport<em>Xxx</em>接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口对象</p></td>
<td align="left"><p>对象公开端口驱动程序的 IPort<em>Xxx</em>接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>资源列表对象</p></td>
<td align="left"><p>一个包含一组适配器驱动程序资源分配给子对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>引用字符串</p></td>
<td align="left"><p>名称添加到要在筛选器创建期间指定子的设备路径名称</p></td>
</tr>
</tbody>
</table>

 

子 IMiniport*Xxx*和 IPort*Xxx*接口继承自基接口[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)并[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)分别。

PortCls 系统驱动程序不区分端口驱动程序和微型端口驱动程序。 它只是需要一个对象，如端口对象，可以处理系统生成的请求的接口。

同样，PortCls 没有直接包括在管理资源。 它只需将请求处理程序 （端口驱动程序） 绑定到资源的列表。 适配器驱动程序负责将端口、 微型端口和资源的列表对象绑定在一起。

下面的代码示例显示了适配器驱动程序如何执行以下操作：

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

在前面的代码示例中调用 PortCls 函数的信息，请参阅[ **PcNewPort**](https://msdn.microsoft.com/library/windows/hardware/ff537715)， [ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)，和[**PcRegisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537731)。

 

 




