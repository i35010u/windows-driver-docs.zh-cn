---
title: 内核模式安全字符串函数摘要
description: 内核模式安全字符串函数摘要
ms.assetid: 71b67d88-2a9a-4c9d-b64c-5fd7fe7e5cda
keywords:
- 安全字符串函数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e413e339807160a7895ee0ffe7185c7d5a62df76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382974"
---
# <a name="summary-of-kernel-mode-safe-string-functions"></a>内核模式安全字符串函数摘要





下表总结了适用于内核模式驱动程序的安全字符串函数，它表示 C /C++语言运行时库函数时，它们替换。 如果函数的名称中包含**Cb**，该函数将字符串视为字节计数。 如果函数的名称中包含**Cch**，该函数将字符串视为字符计数。

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
<th>替换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<dl>
<dt><a href="" id="rtlstringcbcat"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcata" data-raw-source="[&lt;strong&gt;RtlStringCbCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcata)"><strong>RtlStringCbCat</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcatex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatexa)"><strong>RtlStringCbCatEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcat"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcata" data-raw-source="[&lt;strong&gt;RtlStringCchCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcata)"><strong>RtlStringCchCat</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcatex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatexa)"><strong>RtlStringCchCatEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcat"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcat)"><strong>RtlUnicodeStringCat</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcatex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatex)"><strong>RtlUnicodeStringCatEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcatstring"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstring)"><strong>RtlUnicodeStringCatString</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcatstringex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCatStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcatstringex)"><strong>RtlUnicodeStringCatStringEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcatstringn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringn)"><strong>RtlUnicodeStringCbCatStringN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcatstringnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatstringnex)"><strong>RtlUnicodeStringCbCatStringNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcatstringn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringn)"><strong>RtlUnicodeStringCchCatStringN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcatstringnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatstringnex)"><strong>RtlUnicodeStringCchCatStringNEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>串联两个字符串。</p></td>
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
<dt><a href="" id="rtlstringcbcatn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna" data-raw-source="[&lt;strong&gt;RtlStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatna)"><strong>RtlStringCbCatN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcatnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcatnexa)"><strong>RtlStringCbCatNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcatn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna" data-raw-source="[&lt;strong&gt;RtlStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatna)"><strong>RtlStringCchCatN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcatnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa" data-raw-source="[&lt;strong&gt;RtlStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcatnexa)"><strong>RtlStringCchCatNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcatn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatn)"><strong>RtlUnicodeStringCbCatN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcatnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcatnex)"><strong>RtlUnicodeStringCbCatNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcatn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatn)"><strong>RtlUnicodeStringCchCatN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcatnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCatNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcatnex)"><strong>RtlUnicodeStringCchCatNEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>串联两个字节计数字符串时追加的字符串的大小限制。</p></td>
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
<dt><a href="" id="rtlstringcbcopy"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya" data-raw-source="[&lt;strong&gt;RtlStringCbCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopya)"><strong>RtlStringCbCopy</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcopyex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyexa)"><strong>RtlStringCbCopyEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcopyunicodestring"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestring)"><strong>RtlStringCbCopyUnicodeString</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcopyunicodestringex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCbCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyunicodestringex)"><strong>RtlStringCbCopyUnicodeStringEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopy"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya" data-raw-source="[&lt;strong&gt;RtlStringCchCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopya)"><strong>RtlStringCchCopy</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopyex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyexa)"><strong>RtlStringCchCopyEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopyunicodestring"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestring)"><strong>RtlStringCchCopyUnicodeString</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopyunicodestringex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex" data-raw-source="[&lt;strong&gt;RtlStringCchCopyUnicodeStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyunicodestringex)"><strong>RtlStringCchCopyUnicodeStringEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcopy"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopy)"><strong>RtlUnicodeStringCopy</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcopyex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopyex)"><strong>RtlUnicodeStringCopyEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcopystring"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystring)"><strong>RtlUnicodeStringCopyString</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcopystringex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCopyStringEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcopystringex)"><strong>RtlUnicodeStringCopyStringEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>将一个字符串复制到缓冲区。</p></td>
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
<dt><a href="" id="rtlstringcbcopyn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna" data-raw-source="[&lt;strong&gt;RtlStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopyna)"><strong>RtlStringCbCopyN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbcopynex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbcopynexa)"><strong>RtlStringCbCopyNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopyn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna" data-raw-source="[&lt;strong&gt;RtlStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopyna)"><strong>RtlStringCchCopyN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchcopynex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa" data-raw-source="[&lt;strong&gt;RtlStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchcopynexa)"><strong>RtlStringCchCopyNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcopyn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopyn)"><strong>RtlUnicodeStringCbCopyN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcopynex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopynex)"><strong>RtlUnicodeStringCbCopyNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcopyn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopyn)"><strong>RtlUnicodeStringCchCopyN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcopynex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopynex)"><strong>RtlUnicodeStringCchCopyNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcopystringn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringn)"><strong>RtlUnicodeStringCbCopyStringN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcbcopystringnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCbCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcbcopystringnex)"><strong>RtlUnicodeStringCbCopyStringNEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcopystringn"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringn)"><strong>RtlUnicodeStringCchCopyStringN</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringcchcopystringnex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringCchCopyStringNEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringcchcopystringnex)"><strong>RtlUnicodeStringCchCopyStringNEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>将一个字符串到缓冲区中，复制时复制的字符串的大小限制。</p></td>
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
<dt><a href="" id="rtlstringcblength"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha" data-raw-source="[&lt;strong&gt;RtlStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcblengtha)"><strong>RtlStringCbLength</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchlength"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha" data-raw-source="[&lt;strong&gt;RtlStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchlengtha)"><strong>RtlStringCchLength</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunalignedstringcblength"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCbLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcblengthw)"><strong>RtlUnalignedStringCbLength</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunalignedstringcchlength"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw" data-raw-source="[&lt;strong&gt;RtlUnalignedStringCchLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunalignedstringcchlengthw)"><strong>RtlUnalignedStringCchLength</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>确定提供的字符串的长度。</p></td>
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
<dt><a href="" id="rtlstringcbprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfa)"><strong>RtlStringCbPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbprintfexa)"><strong>RtlStringCbPrintfEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfa)"><strong>RtlStringCchPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchprintfexa)"><strong>RtlStringCchPrintfEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintf)"><strong>RtlUnicodeStringPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringprintfex)"><strong>RtlUnicodeStringPrintfEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>创建基于格式字符串和其他函数自变量的一组带格式的文本字符串。</p></td>
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
<dt><a href="" id="rtlstringcbvprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfa)"><strong>RtlStringCbVPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcbvprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCbVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcbvprintfexa)"><strong>RtlStringCbVPrintfEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchvprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfa)"><strong>RtlStringCchVPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlstringcchvprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa" data-raw-source="[&lt;strong&gt;RtlStringCchVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlstringcchvprintfexa)"><strong>RtlStringCchVPrintfEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringvprintf"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintf&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintf)"><strong>RtlUnicodeStringVPrintf</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringvprintfex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringVPrintfEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvprintfex)"><strong>RtlUnicodeStringVPrintfEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>创建基于格式字符串和一个其他函数自变量的带格式的文本字符串。</p></td>
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
<dt><a href="" id="rtlunicodestringinit"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInit&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringinit)"><strong>RtlUnicodeStringInit</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringinitex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringInitEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringinitex)"><strong>RtlUnicodeStringInitEx</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringvalidate"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidate)"><strong>RtlUnicodeStringValidate</strong></a></dt>
<dd>
</dd>
<dt><a href="" id="rtlunicodestringvalidateex"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex" data-raw-source="[&lt;strong&gt;RtlUnicodeStringValidateEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntstrsafe/nf-ntstrsafe-rtlunicodestringvalidateex)"><strong>RtlUnicodeStringValidateEx</strong></a></dt>
<dd>
</dd>
</dl></td>
<td><p>初始化或验证<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string" data-raw-source="[&lt;strong&gt;UNICODE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)"> <strong>UNICODE_STRING</strong> </a>结构。</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




