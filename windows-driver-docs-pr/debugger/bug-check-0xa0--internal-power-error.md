---
title: Bug Check 0xA0 INTERNAL_POWER_ERROR
description: INTERNAL_POWER_ERROR bug 检查具有 0x000000A0 值。 此 bug 检查指示电源策略管理器遇到致命错误。
ms.assetid: a763e865-8591-4ed3-b3cd-1cdaecad6e97
keywords:
- Bug Check 0xA0 INTERNAL_POWER_ERROR
- INTERNAL_POWER_ERROR
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- INTERNAL_POWER_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 043c2a2ab16f79247f451ecfe0340d2b8ac1bcc3
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239852"
---
# <a name="bug-check-0xa0-internalpowererror"></a>Bug 检查 0xA0：INTERNAL\_POWER\_ERROR


内部\_电源\_错误 bug 检查的值为 0x000000A0。 此 bug 检查指示电源策略管理器遇到致命错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="internalpowererror-parameters"></a>内部\_电源\_错误参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p><strong>1:</strong>设备具有溢出其引用计数的最大数。</p>
<p><strong>2、 3 或 4:</strong>已排队 Irp 的浪涌 power 太多。</p>
<p><strong>5:</strong>Power IRP 已发送到被动级别的设备对象。</p>
<p><strong>6:</strong>系统无法分配必要 power IRP。</p></td>
<td align="left"><p>如果参数 2 具有值为 1，引用允许的最大数目。</p>
<p>如果参数 2 的值为 2、 3 或 4，允许挂起的 Irp 的最大数目。</p>
<p>如果参数 2 具有的值为 6，目标设备对象。</p></td>
<td align="left">如果参数 2 值为 6，指示这是否是系统 (0x0) 或设备 (0x1) 电源 IRP。</td>
<td align="left"><p>Power I/O 请求数据包 (IRP) 在处理期间出错。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>尝试处理电源事件时发生了内部错误。 有关详细信息，请参阅<a href="#parameter-1-equals-0x2" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x2](#parameter-1-equals-0x2)">调试 bug 检查当参数 1 等于 0x2 0xA0</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>所需的校验和</p></td>
<td align="left"><p>实际校验和</p></td>
<td align="left"><p>失败的行号</p></td>
<td align="left"><p>休眠上下文页的校验和不匹配其预期的校验和。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>所需的校验和</p></td>
<td align="left"><p>实际校验和</p></td>
<td align="left"><p>失败的行号</p></td>
<td align="left"><p>要写入到休眠文件的页的校验和不匹配其预期的校验和。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>未知的关闭代码已发送到系统关闭处理程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>发生未经处理的异常。 有关详细信息，请参阅<a href="#parameter-1-equals-0x7" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x7](#parameter-1-equals-0x7)">调试 bug 检查当参数 1 等于 0x7 0xA0</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>此参数始终设置为 0x100。</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>POWER_CHANNEL_SUMMARY</p>
<p></p></td>
<td align="left"><p>处理系统电源事件时出错。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>状态代码</p></td>
<td align="left"><p>镜像阶段</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>准备休眠文件时出错。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p><strong>0:</strong>在恢复后立即请求的 bug 检查。</p>
<p><strong>1:</strong>Bug 检查请求期间恢复所有非可分页的设备已开机。</p>
<p><strong>2:</strong>所有设备已都开机后恢复运行时请求的 bug 检查。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>出于调试目的唤醒系统时，已请求的 bug 检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>休眠文件的大小。</p></td>
<td align="left"><p>休眠状态进度，然后再运行空间不足</p>
<p><strong>0:</strong>HIBERFILE_PROGRESS_FREE_MAP</p>
<p><strong>1:</strong>HIBERFILE_PROGRESS_RESUME_CONTEXT</p>
<p><strong>2:</strong>HIBERFILE_PROGRESS_PROCESSOR_STATEE</p>
<p><strong>3:</strong>HIBERFILE_PROGRESS_MEMORY_RANGES</p>
<p><strong>4:</strong>HIBERFILE_PROGRESS_TABLE_PAGES</p>
<p><strong>5:</strong>HIBERFILE_PROGRESS_MEMORY_IMAGE</p></td>
<td align="left"><p>剩余的内存范围的大小。</p></td>
<td align="left"><p>休眠文件是太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xC</p></td>
<td align="left"><p>状态代码</p></td>
<td align="left"><p>转储堆栈上下文</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>转储堆栈初始化失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>异常的指针。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>处理系统电源事件时出现未经处理的异常。 有关详细信息，请参阅<a href="#parameter-1-equals-0x101" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x101](#parameter-1-equals-0x101)">调试 bug 检查当参数 1 等于 0x101 0xA0</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x102</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>DUMP_INITIALIZATION_CONTEXT</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>休眠工作缓冲区大小不是对齐的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x103</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在休眠状态过程中考虑为无法工作的所有页面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x104</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>尝试将内部休眠内存映射的内部内存结构已锁定时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x105</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>尝试将映射内部休眠内存以及不受支持的内存类型标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x106</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>内存描述符列表 (MDL)</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>休眠过程描述为未分页对齐的内存中创建内存描述符列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>PO_MEMORY_RANGE_ARRAY</p></td>
<td align="left"><p>在内部休眠数据结构中出现数据不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>磁盘子系统未能正确写入休眠文件的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>所需校验和</p></td>
<td align="left"><p>实际校验和</p></td>
<td align="left"><p>处理器状态数据的校验和不匹配其预期的校验和。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>磁盘子系统无法正确读取或写入休眠文件的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>当前休眠进度</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>尝试将页面标记为错误的时间使用 PoSetHiberRange API 在休眠状态的启动阶段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>提供给 API 的标志</p></td>
<td align="left"><p>若要将标记的长度</p></td>
<td align="left"><p>调用 PoSetHiberRange API 时使用的参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>DEVICE_OBJECT_POWER_EXTENSION</p></td>
<td align="left"><p>正在为空闲状态检查未知的设备类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x300</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>从电池电源 IRP 返回未知的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x301</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>电池已进入未知的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>IO_STACK_LOCATION</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>设备具有溢出其引用计数的最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x401</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>挂起 IRP 列表</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>已排队 Irp 的浪涌 power 太多。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x402</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>挂起 IRP 列表</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>已排队 Irp 的浪涌 power 太多。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x403</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>挂起 IRP 列表</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>已排队 Irp 的浪涌 power 太多。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>IO_STACK_LOCATION</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>幂 IRP 已发送到被动级别的设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x500</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>从散热电源 IRP 返回未知的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x600</p></td>
<td align="left"><p>DEVICE_OBJECT PDO</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>驱动程序已尝试重复使用电源运行时框架注册。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x601</p></td>
<td align="left"><p>POP_FX_DEVICE 设备</p></td>
<td align="left"><p>PEP_DEVICE_REGISTER PEP</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>任何 Power 引擎插件不接受设备注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x602</p></td>
<td align="left"><p>DEVICE_NODE 设备节点</p></td>
<td align="left"><p>进入睡眠状态计数</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>设备节点睡眠计数不匹配其激活计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x603</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>工作请求类型</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Power 引擎插件所做的无效的工作请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x605</p></td>
<td align="left"><p>通知 ID</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Power 引擎插件无法接受必需的设备电源管理通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x606</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>POP_FX_COMPONENT_FLAGS</p></td>
<td align="left"><p>组件的新条件</p></td>
<td align="left"><p>Power 引擎插件尝试转换活动 （或空闲） 条件的一个关键的系统资源组件资源已为活动 （或空闲） 时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x607</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>运行时电源管理框架设备删除锁定的获取失败时需要它才能成功。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x608</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>POP_FX_COMPONENT_FLAGS</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>驱动程序已尝试转换到空闲而无需前面的活动请求的组件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x609</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>重复的请求类型</p>
<p><strong>0:</strong>DevicePowerRequired</p>
<p><strong>1:</strong>DevicePowerNotRequired</p></td>
<td align="left"><p>Power 引擎插件已请求没有另一类型的干预请求不需要任一设备电源必需或设备电源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x610</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Power 引擎插件已请求不需要同时上一设备电源所需的请求未完成设备电源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x611</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>无效的组件索引</p></td>
<td align="left"><p>Power 引擎插件请求了无效的组件上一个操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x612</p></td>
<td align="left"><p>POP_FX_PLUGIN PowerEnginePlugin</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Power 引擎插件已请求在设备通知，其中没有缓冲区由提供的采购订单请求的上下文中完成其他工作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x613</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>组件索引</p></td>
<td align="left"><p>操作</p>
<p><strong>0:</strong>完成设备电源不是必需的</p>
<p><strong>1:</strong>报告设备上提供支持</p>
<p><strong>2:</strong>完整的空闲条件</p></td>
<td align="left"><p>驱动程序已尝试完成请求时没有此类未完成的请求处于挂起状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x614</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>组件索引</p></td>
<td align="left"><p>非法参数</p>
<p><strong>0:</strong>在 IRQL 使用 PO_FX_FLAG_BLOCKING &gt;= DISPATCH_LEVEL</p>
<p><strong>1:</strong>两个都指定 PO_FX_FLAG_BLOCKING 和 PO_FX_FLAG_ASYNC_ONLY</p>
<p><strong>2:</strong>无效的组件索引</p></td>
<td align="left"><p>驱动程序已请求具有非法的参数的组件上的/空闲处于活动状态的转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x615</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>非法操作</p>
<p><strong>0:</strong>组件未处于空闲状态 0</p>
<p><strong>1:</strong>组件已处于活动状态</p>
<p><strong>2:</strong>任何未完成激活请求</p>
<p><strong>3:</strong>未完成的空闲状态转换</p></td>
<td align="left"><p>Power 引擎插件非法已指明组件激活完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x616</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>非法操作</p>
<p><strong>0:</strong>无效的空闲状态</p>
<p><strong>1:</strong>组件已处于请求的状态</p>
<p><strong>2:</strong>请求非零值空闲状态，而无需通过空闲状态 0</p></td>
<td align="left"><p>Power 引擎插件非法请求组件空闲状态转换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x666</p></td>
<td align="left"><p>PPOP_PEP_ACTIVITY</p></td>
<td align="left"><p>新的活动类型</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>冲突的活动类型</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>默认 Power 引擎插件已尝试触发新的活动与另一个活动的相冲突。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x667</p></td>
<td align="left"><p>POP_PEP_ACTIVITY</p></td>
<td align="left"><p>活动类型</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>POP_PEP_ACTIVITY_STATUS</p></td>
<td align="left"><p>默认 Power 引擎插件已尝试完成未运行的活动。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x700</p></td>
<td align="left"><p>PEPHANDLE</p></td>
<td align="left"><p>PEP_PPM_IDLE_SELECT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Power 引擎插件已指定无效处理器空闲依赖项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x701</p></td>
<td align="left"><p>挂起的处理器的所选空闲状态的索引</p></td>
<td align="left"><p>挂起的处理器的 PRCB 地址</p></td>
<td align="left"><p>挂起的处理器的索引</p></td>
<td align="left"><p>一个处理器无法完成的已分配的时间间隔内的空闲状态转换。 这表示挂起指定的处理器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x702</p></td>
<td align="left"><p>所选的空闲状态的处理器的索引</p></td>
<td align="left"><p>处理器的空闲状态同步状态</p></td>
<td align="left"><p>挂起的处理器的 PRCB 地址</p></td>
<td align="left"><p>一个处理器中唤醒从非可中断状态而无需启动通过 PEP （使用必要的 PPM 空闲同步） 显式唤醒的操作系统。</p></td>
</tr>
</tbody>
</table>





<a name="resolution"></a>分辨率
----------

**常规注释**

在上表中，多个参数是指向结构的指针。 例如，如果参数 2 列为设备\_对象，则参数 2 是指向设备\_对象结构。 Wdm.h 中，包含在 Windows 驱动程序工具包中定义的某些结构。 例如，以下结构中 wdm.h 中定义。

-   异常\_指针
-   设备\_对象
-   IO\_堆栈\_位置
-   PEP\_DEVICE\_REGISTER

在上表中显示的结构的一些未定义任何公共头文件中。 可以使用来查看这些结构的定义[ **dt** ](dt--display-type-.md)调试器命令。 下面的示例演示如何使用**dt**命令，请参阅**设备\_对象\_POWER\_扩展**结构。

```dbgcmd
3: kd> dt nt!DEVICE_OBJECT_POWER_EXTENSION
   +0x000 IdleCount        : Uint4B
   +0x004 BusyCount        : Uint4B
   +0x008 BusyReference    : Uint4B
   +0x00c TotalBusyCount   : Uint4B
   +0x010 ConservationIdleTime : Uint4B
   +0x014 PerformanceIdleTime : Uint4B
   +0x018 DeviceObject     : Ptr64 _DEVICE_OBJECT
   +0x020 IdleList         : _LIST_ENTRY
   +0x030 IdleType         : _POP_DEVICE_IDLE_TYPE
   +0x034 IdleState        : _DEVICE_POWER_STATE
   +0x038 CurrentState     : _DEVICE_POWER_STATE
   +0x040 Volume           : _LIST_ENTRY
   +0x050 Specific         : <unnamed-tag>
```

以下过程将帮助你调试此 bug 检查的特定实例。

<span id="parameter-1-equals-0x2"></span><span id="PARAMETER-1-EQUALS-0X2"></span>
**调试 bug 检查当参数 1 等于 0x2 0xA0**

1.  检查堆栈。 查找**ntoskrnl ！PopExceptionFilter**函数。 此函数作为其第一个参数包含以下代码。

    ```cpp
     (error_code << 16) | _LINE_
    ```

    如果调用方**PopExceptionFilter**，此函数的第一个参数属于类型 PEXCEPTION\_指针。 请注意此自变量的值。

2.  使用[ **dt （显示类型）** ](dt--display-type-.md)命令并指定为在上一步中找到的值*参数*。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    此命令显示的结构。 请注意上下文记录的地址。

3.  使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令并指定为在上一步中找到的上下文记录*记录*。

    ```dbgcmd
    .cxr record 
    ```

    此命令将寄存器上下文设置为正确的值。

4.  使用不同的命令分析错误的源。 开头[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 。

<span id="parameter-1-equals-0x7"></span><span id="PARAMETER-1-EQUALS-0X7"></span>
**调试 bug 检查当参数 1 等于 0x7 0xA0**

1.  检查堆栈。 查找**ntoskrnl ！PopExceptionFilter**函数。 此函数的第一个参数属于类型 PEXCEPTION\_指针。 请注意此自变量的值。

2.  使用[ **dt （显示类型）** ](dt--display-type-.md)命令并指定为在上一步中找到的值*参数*。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    此命令显示的结构。 请注意上下文记录的地址。

3.  使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令并指定为在上一步中找到的上下文记录*记录*。

    ```dbgcmd
    .cxr record 
    ```

    此命令将寄存器上下文设置为正确的值。

4.  使用不同的命令分析错误的源。 开头[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 。

<span id="parameter-1-equals-0x101"></span><span id="PARAMETER-1-EQUALS-0X101"></span>
**调试 bug 检查当参数 1 等于 0x101 0xA0**

1.  使用[ **dt （显示类型）** ](dt--display-type-.md)命令并指定为参数 3 的值*参数*。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    此命令显示的结构。 请注意上下文记录的地址。

2.  使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令并指定找到为在上一步的上下文记录*记录*。

    ```dbgcmd
    .cxr record 
    ```

    此命令将寄存器上下文设置为正确的值。

3.  使用不同的命令分析错误的源。 开头[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 。

 

 




