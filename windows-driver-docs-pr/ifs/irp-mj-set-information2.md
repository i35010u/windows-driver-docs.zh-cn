---
title: 正在检查 IRP_MJ_SET_INFORMATION 操作 Oplock 状态
description: 正在检查 IRP_MJ_SET_INFORMATION 操作 Oplock 状态
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d00b47675e9af7846e588c859278c8ecc5f6042
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348598"
---
# <a name="checking-the-oplock-state-of-an-irpmjsetinformation-operation"></a>正在检查 IRP_MJ_SET_INFORMATION 操作 Oplock 状态


某些 IRP_MJ_SET_INFORMATION 操作检查 oplock 状态。 以下六个操作执行此检查：

### <a name="span-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanspan-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanspan-idfileendoffileinformationfileallocationinformationandfilevaliddatalengthinformationspanfileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation"></a><span id="FileEndOfFileInformation__FileAllocationInformation__and_FileValidDataLengthInformation"></span><span id="fileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformation"></span><span id="FILEENDOFFILEINFORMATION__FILEALLOCATIONINFORMATION__AND_FILEVALIDDATALENGTHINFORMATION"></span>FileEndOfFileInformation、 FileAllocationInformation 和 FileValidDataLengthInformation

此信息适用于文件或流上执行以下操作：

- 调用方尝试更改该流的逻辑大小。 请注意，当缓存管理器的惰性编写器线程尝试设置新的文件结尾，不 oplock 进行检查。 这是因为接收实际写入请求时之前进行检查。

- 调用方尝试更改该流的分配的大小。
  <table>
  <tr>
  <th>请求类型</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>级别 1</p>
  <p>Batch</p>
  <p>Filter</p>
  <p>读取句柄</p>
  <p>读写</p>
  <p>读写句柄</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileEndOfFileInformtion、 FileAllocationInformation 和 FileValidDataLengthInformation） 时：</p>
  <ul>
  <li>
  <p> 该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p> 中断为无。</p>
  </li>
  <li>
  <p>读取句柄请求：尽管需要确认该中断，则操作将立即继续 （即，而无需等待确认）。</p>
  </li>
  <li>
  <p> 对于所有其他请求类型：继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>Read</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileEndOfFileInformtion、 FileAllocationInformation 和 FileValidDataLengthInformation） 时：</p>
  <ul>
  <li>
  <p> 该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p> 中断为无。</p>
  </li>
  <li>
  <p> 不发送任何确认是必需的可以立即继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>级别 2</p>
  </td>
  <td>
  <ul>
  <li>
  <p> 为无始终中断。</p>
  </li>
  <li>
  <p> 不发送任何确认是必需的可以立即继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileRenameInformation__FileShortNameInformation__and_FileLinkInformation"></a><a id="filerenameinformation__fileshortnameinformation__and_filelinkinformation"></a><a id="FILERENAMEINFORMATION__FILESHORTNAMEINFORMATION__AND_FILELINKINFORMATION"></a>FileRenameInformation、 FileShortNameInformation 和 FileLinkInformation</h3>
  <p>此信息适用于文件或流上执行以下操作：</p>
  <ul>
  <li>
  <p> 要重命名文件或流。</p>
  </li>
  <li>
  <p> 为文件设置的短名称。</p>
  </li>
  <li>
  <p> 正在为文件创建硬链接。 这会影响 oplock 状态，如果新的硬链接取代现有链接到另一个文件，并且将其取代的链接上存在 oplock。</p>
  </li>
  <li>
  <p> 正在重命名的机会锁存在于其的流的上级目录，或要设置的上级目录的短名称。</p>
  </li>
  </ul>
  <table>
  <tr>
  <th>请求类型</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>Batch</p>
  <p>Filter</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、 FileShortNameInformation 和 FileLinkInformation） 时：</p>
  <ul>
  <li>
  <p>  该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> 如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p>  中断为无。</p>
  </li>
  <li>
  <p> 继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读取句柄</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、 FileShortNameInformation 和 FileLinkInformation） 时：</p>
  <ul>
  <li>
  <p>  该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> 如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p>  中断到读取。</p>
  </li>
  <li>
  <p> 继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读写句柄</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、 FileShortNameInformation 和 FileLinkInformation） 时：</p>
  <ul>
  <li>
  <p> 该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p> 中断到读写。</p>
  </li>
  <li>
  <p> 继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>级别 1</p>
  <p>级别 2</p>
  <p>Read</p>
  <p>读写</p>
  </td>
  <td>
  <ul>
  <li>
  <p> 就不会破坏 oplock，不发送任何确认是必需的可以立即继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileDispositionInformation"></a><a id="filedispositioninformation"></a><a id="FILEDISPOSITIONINFORMATION"></a>FileDispositionInformation</h3>
  <p>此信息适用于调用方尝试删除该文件。</p>
  <table>
  <tr>
  <th>请求类型</th>
  <th>条件</th>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读取句柄</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileDispositionInformation) 时：</p>
  <ul>
  <li>
  <p>该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  <p><b>AND</b></p>
  </li>
  <li>
  <p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545765"><b>FILE_DISPOSITION_INFORMATION</b></a>。是 DeleteFile <b>，则返回 TRUE</b>。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p> 中断到读取。</p>
  </li>
  <li>
  <p>继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读写句柄</p>
  </td>
  <td>
  <p>上中断 IRP_MJ_SET_INFORMATION （适用于 FileDispositionInformation) 时：</p>
  <ul>
  <li>
  <p>该操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
  <p><b>AND</b></p>
  </li>
  <li>
  <p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545765"><b>FILE_DISPOSITION_INFORMATION</b></a>。是 DeleteFile <b>，则返回 TRUE</b>。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 已损坏：</p>
  <ul>
  <li>
  <p> 中断到读写。</p>
  </li>
  <li>
  <p>继续操作之前必须收到确认。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
 




