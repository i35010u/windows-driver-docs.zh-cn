---
title: 检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态
description: 检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态
ms.assetid: d164be8d-cf42-4b96-9883-e0f8223bfde4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caacea027897c13c5114b2d515636a232a452f39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841149"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_set_information-operation"></a>检查 IRP_MJ_SET_INFORMATION 操作的 Oplock 状态


某些 IRP_MJ_SET_INFORMATION 操作检查 oplock 状态。 以下六个操作执行此检查：

### <a name="span-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanspan-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanspan-idfileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformationspanfileendoffileinformation-fileallocationinformation-and-filevaliddatalengthinformation"></a><span id="FileEndOfFileInformation__FileAllocationInformation__and_FileValidDataLengthInformation"></span><span id="fileendoffileinformation__fileallocationinformation__and_filevaliddatalengthinformation"></span><span id="FILEENDOFFILEINFORMATION__FILEALLOCATIONINFORMATION__AND_FILEVALIDDATALENGTHINFORMATION"></span>FileEndOfFileInformation、FileAllocationInformation 和 FileValidDataLengthInformation

此信息适用于对文件或流执行以下操作：

- 调用方尝试更改流的逻辑大小。 请注意，当缓存管理器的惰性编写器线程尝试设置新的文件尾时，不进行任何 oplock 检查。 这是因为，在接收到实际的写入请求时，会进行此检查。

- 调用方尝试更改流的分配大小。
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
  <p>读写-句柄</p>
  </td>
  <td>
  <p>在以下情况下，IRP_MJ_SET_INFORMATION （适用于 FileEndOfFileInformtion、FileAllocationInformation 和 FileValidDataLengthInformation）中断：</p>
  <ul>
  <li>
  <p> 该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 中断：</p>
  <ul>
  <li>
  <p> 中断到无。</p>
  </li>
  <li>
  <p>对于读取句柄请求：尽管需要确认中断，但操作会立即继续（即，无需等待确认）。</p>
  </li>
  <li>
  <p> 对于所有其他请求类型：必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>已阅读</p>
  </td>
  <td>
  <p>在以下情况下，IRP_MJ_SET_INFORMATION （适用于 FileEndOfFileInformtion、FileAllocationInformation 和 FileValidDataLengthInformation）中断：</p>
  <ul>
  <li>
  <p> 该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 中断：</p>
  <ul>
  <li>
  <p> 中断到无。</p>
  </li>
  <li>
  <p> 不需要确认，操作会立即继续。</p>
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
  <p> 始终中断到无。</p>
  </li>
  <li>
  <p> 不需要确认，操作会立即继续。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileRenameInformation__FileShortNameInformation__and_FileLinkInformation"></a><a id="filerenameinformation__fileshortnameinformation__and_filelinkinformation"></a><a id="FILERENAMEINFORMATION__FILESHORTNAMEINFORMATION__AND_FILELINKINFORMATION"></a>FileRenameInformation、FileShortNameInformation 和 FileLinkInformation</h3>
  <p>此信息适用于对文件或流执行以下操作：</p>
  <ul>
  <li>
  <p> 正在重命名文件或流。</p>
  </li>
  <li>
  <p> 正在为文件设置短名称。</p>
  </li>
  <li>
  <p> 正在为文件创建硬链接。 如果新的硬链接取代了到其他文件的现有链接，并在被取代的链接上存在 oplock，则这会影响 oplock 状态。</p>
  </li>
  <li>
  <p> 正在重命名其锁定的流的祖先目录，或正在设置祖先目录的短名称。</p>
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
  <p>在以下情况下，IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、FileShortNameInformation 和 FileLinkInformation）中断：</p>
  <ul>
  <li>
  <p>  该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> 如果 oplock 中断：</p>
  <ul>
  <li>
  <p>  中断到无。</p>
  </li>
  <li>
  <p> 必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读取句柄</p>
  </td>
  <td>
  <p>在以下情况下，IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、FileShortNameInformation 和 FileLinkInformation）中断：</p>
  <ul>
  <li>
  <p>  该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p> 如果 oplock 中断：</p>
  <ul>
  <li>
  <p>  要读取的断点。</p>
  </li>
  <li>
  <p> 必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读写-句柄</p>
  </td>
  <td>
  <p>在以下情况下，IRP_MJ_SET_INFORMATION （适用于 FileRenameInformation、FileShortNameInformation 和 FileLinkInformation）中断：</p>
  <ul>
  <li>
  <p> 该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 中断：</p>
  <ul>
  <li>
  <p> 中断以进行读写。</p>
  </li>
  <li>
  <p> 必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>级别 1</p>
  <p>级别 2</p>
  <p>已阅读</p>
  <p>读写</p>
  </td>
  <td>
  <ul>
  <li>
  <p> Oplock 不会中断，无需确认，操作会立即继续。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
  <p> </p>
  <h3><a id="FileDispositionInformation"></a><a id="filedispositioninformation"></a><a id="FILEDISPOSITIONINFORMATION"></a>FileDispositionInformation</h3>
  <p>当调用方尝试删除文件时，将应用此信息。</p>
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
  <p>发生以下情况时，在 IRP_MJ_SET_INFORMATION （对于 FileDispositionInformation）中断：</p>
  <ul>
  <li>
  <p>该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  <p><b>与</b></p>
  </li>
  <li>
  <p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information"><b>FILE_DISPOSITION_INFORMATION</b></a>。DeleteFile 为<b>TRUE</b>。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 中断：</p>
  <ul>
  <li>
  <p> 要读取的断点。</p>
  </li>
  <li>
  <p>必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td rowspan="2">
  <p>读写-句柄</p>
  </td>
  <td>
  <p>发生以下情况时，在 IRP_MJ_SET_INFORMATION （对于 FileDispositionInformation）中断：</p>
  <ul>
  <li>
  <p>该操作在具有不同的 oplock 密钥的 FILE_OBJECT 上发生，该 FILE_OBJECT 拥有 oplock。</p>
  <p><b>与</b></p>
  </li>
  <li>
  <p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_disposition_information"><b>FILE_DISPOSITION_INFORMATION</b></a>。DeleteFile 为<b>TRUE</b>。</p>
  </li>
  </ul>
  </td>
  </tr>
  <tr>
  <td>
  <p>如果 oplock 中断：</p>
  <ul>
  <li>
  <p> 中断以进行读写。</p>
  </li>
  <li>
  <p>必须先收到确认，然后才能继续操作。</p>
  </li>
  </ul>
  </td>
  </tr>
  </table>
 




