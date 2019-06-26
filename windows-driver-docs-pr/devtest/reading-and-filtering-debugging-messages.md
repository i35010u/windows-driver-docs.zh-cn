---
title: 读取和筛选调试消息
description: 读取和筛选调试消息
ms.assetid: 2ad320f6-596d-4b4c-bfad-d570c856bcc7
keywords:
- 调试代码 WDK，读取消息
- 调试代码 WDK，筛选消息
- 读取调试消息
- 筛选调试消息 WDK
- 调试例程 WDK，消息筛选
- 筛选器掩码 WDK 调试
- 组件名称 WDK 调试
- 重要性位域 WDK 调试
- 级别 WDK 调试
- 级别的参数
- 显示调试消息
- 确定优先级调试消息 WDK
- DbgPrint 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3230c3ac3ca27b5882a376fd544bd53057cddaaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356392"
---
# <a name="reading-and-filtering-debugging-messages"></a>读取和筛选调试消息


## <span id="ddk_reading_and_filtering_debugging_messages_tools"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_TOOLS"></span>


[ **DbgPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprintex)， [ **vDbgPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-vdbgprintex)， [ **vDbgPrintExWithPrefix** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-vdbgprintexwithprefix)，并[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)例程将消息发送到你指定的条件下内核调试程序。 此过程使你可以筛选出低优先级的消息。

**请注意**  在 Microsoft Windows Server 2003 和早期版本的 Windows， [ **DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)并[ **KdPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprint)例程将消息无条件地发送到内核调试程序。 在 Windows Vista 和更高版本的 Windows，这些例程发送消息，有条件地，如**DbgPrintEx**并**KdPrintEx**。 使用任何版本的 Windows，您应使用**DbgPrintEx**， **vDbgPrintEx**， **vDbgPrintExWithPrefix**，和**KdPrintEx**，因为这些例程，您可以控制在其下发送消息的条件。

 

**若要筛选调试消息**

1.  对于每个你想要将发送到调试器的消息，使用**DbgPrintEx**， **vDbgPrintEx**， **vDbgPrintExWithPrefix**，或者**KdPrintEx**在您的驱动程序的代码。 合适的组件将名称传递给*ComponentId*参数和值传递到*级别*反映严重性或此消息的性质的参数。 消息本身传递给*格式*并*自变量*参数使用与相同的语法**printf**。

2.  将相应的值设置*组件筛选器掩码*。 每个组件都有不同的掩码。 掩码值指示该组件的消息所示。 您可以设置组件的筛选器掩码注册表中使用注册表编辑器或在内存中使用内核调试程序。

3.  将内核调试程序附加到计算机。 每当您的驱动程序将传递到一条消息时， **DbgPrintEx**， **vDbgPrintEx**， **vDbgPrintExWithPrefix**，或者**KdPrintEx**、值传递给*ComponentId*并*级别*与相应的组件筛选器掩码的值进行比较。 如果这些值都满足特定条件，该消息发送到内核调试程序并显示。 否则，不发送任何消息。

有关完整说明，请参阅以下部分。

**请注意**  到此页上的所有引用**DbgPrintEx**同样适用于**KdPrintEx**， **vDbgPrintEx**，和**vDbgPrintExWithPrefix**。

 

-   [用于标识组件名称](#identifying-the-component-name)
-   [选择正确的级别](#choosing-the-correct-level)
-   [设置组件的筛选器掩码](#setting-the-component-filter-mask)
-   [用于显示消息的条件](#criteria-for-displaying-the-message)
-   [示例](#example)
-   [DbgPrint 缓冲区和调试器](#dbgprint-buffer-and-the-debugger)

### <a name="identifying-the-component-name"></a>用于标识组件名称

每个组件都有单独的筛选器掩码。 此掩码使调试器能够单独配置每个组件的筛选器。

每个组件即为不同的方式，具体取决于上下文。 在中*ComponentId*的参数**DbgPrintEx**，组件名称带有前缀"DPFLTR\_"和与后缀"\_ID"。 在注册表中，组件筛选器掩码必须与组件本身相同的名称。 在调试器中，组件筛选器掩码前缀为"Kd\_"和与后缀"\_掩码"。

组件名称的完整列表 (在 DPFLTR\_*XXXX*\_ID 格式) Dpfilter.h 标头文件中 Windows Driver Kit (WDK) 中。 大多数这些组件名称被保留的用于 Windows 和由 Microsoft 编写的驱动程序。

有六个独立硬件供应商保留的组件名称。 若要避免混合驱动程序的输出与 Windows 组件的输出，应使用以下组件名称之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件名称</th>
<th align="left">驱动程序类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IHVVIDEO</p></td>
<td align="left"><p>视频驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVAUDIO</p></td>
<td align="left"><p>音频驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVNETWORK</p></td>
<td align="left"><p>网络驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVSTREAMING</p></td>
<td align="left"><p>内核流式处理驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVBUS</p></td>
<td align="left"><p>总线驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVDRIVER</p></td>
<td align="left"><p>任何其他类型的驱动程序</p></td>
</tr>
</tbody>
</table>

 

例如，如果你正在编写的视频驱动程序，则会使用 DPFLTR\_IHVVIDEO\_ID 作为*ComponentId*参数**DbgPrintEx**，使用名称中的 IHVVIDEO 值注册表中，和是指**Kd\_IHVVIDEO\_掩码**在调试器中。

在 Windows Vista 和更高版本的 Windows 中，所有消息**DbgPrint**并**KdPrint**发送与相关联的默认组件 (DPFLTR\_默认\_ID)。

### <a name="choosing-the-correct-level"></a>选择正确的级别

*级别*的参数**DbgPrintEx**例程是类型为 DWORD。 要使用它来确定*重要性位域*。 之间的连接*级别*参数和此位域上的大小取决于*级别*:

-   如果*级别*等于 0 到 31，非独占，重要性位域被解释为位移位之间的数字。 重要性位域设置为值 1 &lt; &lt; *级别*。 因此，如果您选择介于 0 到 31 个*级别*，位域都有完全一位组。 如果*级别*为 0，则位域是等效于 0x00000001。 如果*级别*为 31，位域为等效于 0x80000000。

-   如果*级别*是介于 32 和非独占，重要性位域设置的值为 0xFFFFFFFF*级别*本身。

因此，如果你想要设置为 0x00004000 的位域，则可以指定*级别*作为 0x00004000 或只需为 14。 此系统中，因此某些位域值不能生成-包括一组完全为零的标志。

以下常量也可用于设置的值*级别*。 定义 Dpfilter.h WDK 标头文件中：

```ManagedCPlusPlus
#define DPFLTR_ERROR_LEVEL 0
#define DPFLTR_WARNING_LEVEL 1
#define DPFLTR_TRACE_LEVEL 2
#define DPFLTR_INFO_LEVEL 3
#define DPFLTR_MASK 0x80000000
```

一种简单方法使用*级别*参数是始终使用值介于 0 到 31-DPFLTR 由给定的含义与使用的位 0、 1、 2 和 3 之间\_*XXXX*\_级别，并使用表示选择的任何其他位。

使用的另一个简单办法*级别*参数是始终使用显式的位域。 如果选择此方法，您可能想要使用 DPFLTR 的值的按位 OR\_与你的位域的掩码。 此值可确保，你不会意外地使用小于 32 的值。

若要使您的驱动程序兼容于 Windows 使用消息级别的方式，应设置仅最低位 (0x1) 的重要性位域如果发生严重错误。 如果使用的*级别*值小于 32，此值对应于 DPFLTR\_错误\_级别。 如果设置重要性位域，任何人将内核调试程序附加到正在其运行您的驱动程序的计算机的时间将查看您的消息。

使用中适当的情况下的警告、 跟踪和信息级别。 出于任何目的，您有帮助，可以使用其他位。 此功能可以有各种不同的消息类型，可以有选择地显示或隐藏。

在 Windows Vista 和更高版本的 Windows 中，所有消息都发送**DbgPrint**并**KdPrint**行为类似于**DbgPrintEx**和**KdPrintEx**消息*级别*等于 DPFLTR\_信息\_级别。 换而言之，这些消息将第三个位其重要性位域的设置。

### <a name="setting-the-component-filter-mask"></a>设置组件的筛选器掩码

有两种方法来设置组件筛选器掩码：

- 在目标计算机，您可以访问注册表项中的组件筛选器掩码**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\调试打印筛选器**。 使用注册表编辑器，创建或打开此密钥。 在此项下创建一个值中含有大写字母的所需组件的名称 (例如，**默认**或**IHVDRIVER**)。 将此值设置为你想要使用作为组件筛选器掩码的 DWORD 值 (例如，0x8 显示 DPFLTR\_信息\_级别的消息，除了 DPFLTR\_错误\_级别，或将掩码设置为到 0xF显示所有消息）。

- 如果内核调试程序处于活动状态，它可以通过取消引用存储在符号中的地址来访问组件筛选器掩码值**Kd\_** <em>XXXX</em>  **\_掩码**，其中*XXXX*是所需的组件名称。 可以在 WinDbg 或与 KD 显示此掩码的值**dd (显示 DWORD)** 命令，或输入一个新的组件筛选器掩码与**ed (输入 DWORD)** 命令。 如果符号不明确的危险，你可能想要指定此符号作为**nt ！Kd\_** <em>XXXX</em> **\_掩码**。

存储在注册表中的筛选器掩码在启动过程才会生效。 由调试器创建的筛选器掩码会立即生效，并一直持续，直到重新启动目标计算机。 调试器可以重写在注册表中，设置一个值，但如果重新启动目标计算机注册表中指定的值返回组件筛选器掩码。

此外提供了名为 WIN2000 的系统级掩码。 默认情况下，此掩码等于 0x1，但您可以通过注册表或其他组件一样调试程序进行更改。 执行筛选时，每个组件筛选器掩码是第一次组合在一起 WIN2000 子网掩码的按位 OR。 具体而言，这种组合表示永远不会被其掩码的组件指定默认值为 0x1。

### <a name="criteria-for-displaying-the-message"></a>用于显示消息的条件

当**DbgPrintEx**称为在内核模式代码中，Windows 将进行比较的指定消息重要性位域*级别*与由指定组件的筛选器掩码*ComponentId*。

**请注意**  回想一下，当*级别*参数是 0 到 31 之间，重要性位域是等于 1 &lt; &lt; *级别*。 但当*级别*参数为 32 个或更高版本，只需等于重要性位域*级别*。

 

Windows 执行 AND 运算重要性位域和组件筛选器掩码。 如果结果为非零值，该消息发送到调试器。

### <a name="example"></a>示例

假定在上一次启动之前, 已创建中的以下值**调试打印筛选器**密钥：

-   IHVVIDEO，其值等于 DWORD 0x2。

-   IHVBUS，等于 DWORD 0x7FF。

现在您发出内核调试程序中的以下命令：

```
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

此时，IHVVIDEO 组件的筛选器掩码是 0x8，IHVAUDIO 组件的筛选器掩码是 0x7，并且 IHVBUS 组件 0x7FF 的筛选器掩码。

但是，因为这些掩码自动与组合 WIN2000 系统级掩码 （这是通常等于 0x1） 通过使用位或运算，是等效于 0x9 IHVVIDEO 掩码。 未完全设置其筛选器掩码的组件 （例如，IHVSTREAMING 或默认） 已将筛选器掩码设置为 0x1。

现在，假设以下函数调用发生在各种驱动程序：

```
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

第一条消息及其*级别*参数等于 DPFLTR\_信息\_级别，这是 3。 由于此值是小于 32，则将其视为移位，从而导致 0x8 重要性位域。 此值然后结合了 0x9 的有效 IHVVIDEO 组件筛选器掩码使用 AND 运算，给出非零结果。 因此，第一条消息将传送到调试器中。

第二个消息具有其*级别*参数等于 7。 同样，此值被视为移位，从而导致 0x80 重要性位域。 此值然后结合了 0x7 IHVAUDIO 组件筛选器掩码使用 AND 运算，给出零结果。 因此第二条消息不会传输。

第三个消息具有其*级别*参数等于 DPFLTR\_掩码 | 0x10。 此值大于 31，并因此重要性位域设置的值相等*级别*-换而言之，到 0x80000010。 此值然后结合了 0x7FF IHVBUS 组件筛选器掩码使用 AND 运算，给出非零结果。 因此，第三个消息将传送到调试器中。

第四个消息传递给**DbgPrint**而不是例行**DbgPrintEx**例程。 在 Windows Server 2003 和早期版本的 Windows，消息传递给**DbgPrint**始终传输。 在 Windows Vista 和更高版本的 Windows，消息传递给**DbgPrint**总是会获得默认筛选器。 重要性位域是否等于 1 &lt; &lt; DPFLTR\_信息\_级别，即 0x00000008。 此例程的组件是默认值。 由于您尚未设置默认组件筛选器掩码，它具有值为 0x1。 此掩码结合使用 AND 运算的重要性位域，则结果为零。 因此不会传输的第四个消息。

### <a name="dbgprint-buffer-and-the-debugger"></a>DbgPrint 缓冲区和调试器

当**DbgPrint**， **DbgPrintEx**， **vDbgPrintEx**， **vDbgPrintExWithPrefix**， **KdPrint**，或**KdPrintEx**例程到调试器的消息传送，带格式的字符串发送到**DbgPrint**缓冲区。 此缓冲区的内容会立即显示在调试器命令窗口中，除非通过禁用此显示，否则**缓冲区 DbgPrint 输出**GFlags 选项。

如果禁用此显示，您可以查看 DbgPrint 缓冲区的内容，只能通过使用 **！ dbgprint**扩展命令。 有关调试器扩展的信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

调用的任何单个**DbgPrint**， **DbgPrintEx**， **vDbgPrintEx**， **vDbgPrintExWithPrefix**， **KdPrint**，或**KdPrintEx**传输仅 512 个字节的信息。 任何输出长度超过 512 个字节都将丢失。 DbgPrint 缓冲区本身可以免费版本的 Windows，保存最多 4 KB 的数据，并为 32 KB 的数据在签入生成的 Windows。 在 Windows Server 2003 和更高版本的 Windows 上，您可以使用 KDbgCtrl 工具更改 DbgPrint 缓冲区的大小。 此工具是为 Windows 调试工具的一部分。

如果一条消息由于筛选出其*ComponentId*并*级别*值，通过调试连接不会传输。 因此，没有任何办法来在调试器中显示此消息。

 

 





