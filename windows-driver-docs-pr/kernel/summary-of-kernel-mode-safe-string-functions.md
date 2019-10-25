---
title: 内核模式安全字符串函数摘要
description: 内核模式安全字符串函数摘要
ms.assetid: 71b67d88-2a9a-4c9d-b64c-5fd7fe7e5cda
keywords:
- 安全字符串函数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 333d6d54eae985508c8bc3360cc7a88b21b27319
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836223"
---
# <a name="summary-of-kernel-mode-safe-string-functions"></a>内核模式安全字符串函数摘要





下表汇总了可用于内核模式驱动程序的安全字符串函数，并指示它们所替换的 C/C++语言运行库函数。 如果函数的名称包含**Cb**，则函数将字符串视为字节计数。 如果函数的名称包含**Cch**，则函数将字符串视为字符计数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>用途</th>
<th>代替</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata" data-raw-source="[&lt;strong&gt;RtlStringCbCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)"></a></a>RtlStringCbCat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa)"></a></a>RtlStringCbCatEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata" data-raw-source="[&lt;strong&gt;RtlStringCchCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcata)"></a></a>RtlStringCchCat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa)"></a></a>RtlStringCchCatEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcat"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat)"></a></a>RtlUnicodeStringCat</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex)"></a></a>RtlUnicodeStringCatEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatstring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring)"></a></a>RtlUnicodeStringCatString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcatstringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex)"></a></a>RtlUnicodeStringCatStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatstringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn)"></a></a>RtlUnicodeStringCbCatStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatstringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex)"></a></a>RtlUnicodeStringCbCatStringNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatstringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn)"></a></a>RtlUnicodeStringCchCatStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatstringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex)"></a></a>RtlUnicodeStringCchCatStringNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>连接两个字符串。</p></td>
<td><p></p>
<dl>
<dt><strong>strcat</strong></dt>
<dd>
</dd>
<dt><strong>wcscat</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna" data-raw-source="[&lt;strong&gt;RtlStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna)"></a></a>RtlStringCbCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa)"></a></a>RtlStringCbCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna" data-raw-source="[&lt;strong&gt;RtlStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna)"></a></a>RtlStringCchCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa)"></a></a>RtlStringCchCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn)"></a></a>RtlUnicodeStringCbCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex)"></a></a>RtlUnicodeStringCbCatNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn)"></a></a>RtlUnicodeStringCchCatN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcatnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex)"></a></a>RtlUnicodeStringCchCatNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>连接两个字节计数的字符串，同时限制附加字符串的大小。</p></td>
<td><p></p>
<dl>
<dt><strong>strncat</strong></dt>
<dd>
</dd>
<dt><strong>wcsncat</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya" data-raw-source="[&lt;strong&gt;RtlStringCbCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya)"></a></a>RtlStringCbCopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa)"></a></a>RtlStringCbCopyEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyunicodestring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring)"></a></a>RtlStringCbCopyUnicodeString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopyunicodestringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex)"></a></a>RtlStringCbCopyUnicodeStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya" data-raw-source="[&lt;strong&gt;RtlStringCchCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya)"></a></a>RtlStringCchCopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa)"></a></a>RtlStringCchCopyEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyunicodestring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring)"></a></a>RtlStringCchCopyUnicodeString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyunicodestringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex)"></a></a>RtlStringCchCopyUnicodeStringEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopy"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy)"></a></a>RtlUnicodeStringCopy</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopyex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex)"></a></a>RtlUnicodeStringCopyEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopystring"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring)"></a></a>RtlUnicodeStringCopyString</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcopystringex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex)"></a></a>RtlUnicodeStringCopyStringEx</dt>
<dd>
</dd>
</dl></td>
<td><p>将字符串复制到缓冲区中。</p></td>
<td><p></p>
<dl>
<dt><strong>strcpy</strong></dt>
<dd>
</dd>
<dt><strong>wcscpy</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna" data-raw-source="[&lt;strong&gt;RtlStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna)"></a></a>RtlStringCbCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa)"></a></a>RtlStringCbCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna" data-raw-source="[&lt;strong&gt;RtlStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna)"></a></a>RtlStringCchCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa)"></a></a>RtlStringCchCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn)"></a></a>RtlUnicodeStringCbCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex)"></a></a>RtlUnicodeStringCbCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopyn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn)"></a></a>RtlUnicodeStringCchCopyN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopynex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex)"></a></a>RtlUnicodeStringCchCopyNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopystringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn)"></a></a>RtlUnicodeStringCbCopyStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcbcopystringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex)"></a></a>RtlUnicodeStringCbCopyStringNEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopystringn"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn)"></a></a>RtlUnicodeStringCchCopyStringN</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringcchcopystringnex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex)"></a></a>RtlUnicodeStringCchCopyStringNEx</dt>
<dd>
</dd>
</dl></td>
<td><p>将字符串复制到缓冲区，同时限制复制的字符串的大小。</p></td>
<td><p></p>
<dl>
<dt><strong>strncpy</strong></dt>
<dd>
</dd>
<dt><strong>wcsncpy</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcblength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha" data-raw-source="[&lt;strong&gt;RtlStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha)"></a></a>RtlStringCbLength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchlength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha" data-raw-source="[&lt;strong&gt;RtlStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha)"></a></a>RtlStringCchLength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunalignedstringcblength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw)"></a></a>RtlUnalignedStringCbLength</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunalignedstringcchlength"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw)"></a></a>RtlUnalignedStringCchLength</dt>
<dd>
</dd>
</dl></td>
<td><p>确定所提供的字符串的长度。</p></td>
<td><p></p>
<dl>
<dt><strong>strlen</strong></dt>
<dd>
</dd>
<dt><strong>wcslen</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa)"></a></a>RtlStringCbPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa)"></a></a>RtlStringCbPrintfEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa)"></a></a>RtlStringCchPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa)"></a></a>RtlStringCchPrintfEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf)"></a></a>RtlUnicodeStringPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex)"></a></a>RtlUnicodeStringPrintfEx</dt>
<dd>
</dd>
</dl></td>
<td><p>创建基于格式字符串和一组附加函数参数的格式化文本字符串。</p></td>
<td><p></p>
<dl>
<dt><strong>sprintf</strong></dt>
<dd>
</dd>
<dt><strong>swprintf</strong></dt>
<dd>
</dd>
<dt><strong>_snprintf</strong></dt>
<dd>
</dd>
<dt><strong>_snwprintf</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlstringcbvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa)"></a></a>RtlStringCbVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcbvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa)"></a></a>RtlStringCbVPrintfEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa)"></a></a>RtlStringCchVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlstringcchvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa)"></a></a>RtlStringCchVPrintfEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvprintf"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf)"></a></a>RtlUnicodeStringVPrintf</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvprintfex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex)"></a></a>RtlUnicodeStringVPrintfEx</dt>
<dd>
</dd>
</dl></td>
<td><p>创建基于格式字符串和一个附加函数参数的格式化文本字符串。</p></td>
<td><p></p>
<dl>
<dt><strong>vsprintf</strong></dt>
<dd>
</dd>
<dt><strong>vswprintf</strong></dt>
<dd>
</dd>
<dt><strong>_vsnprintf</strong></dt>
<dd>
</dd>
<dt><strong>_vsnwprintf</strong></dt>
<dd>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlunicodestringinit"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInit&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit)"></a></a>RtlUnicodeStringInit</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringinitex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInitEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex)"></a></a>RtlUnicodeStringInitEx</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvalidate"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate)"></a></a>RtlUnicodeStringValidate</dt>
<dd>
</dd>
<dt> <a href="" id="rtlunicodestringvalidateex"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidateEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex)"></a></a>RtlUnicodeStringValidateEx</dt>
<dd>
</dd>
</dl></td>
<td><p>初始化或验证<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string" data-raw-source="[&lt;strong&gt;UNICODE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)"><strong>UNICODE_STRING</strong></a>结构。</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




