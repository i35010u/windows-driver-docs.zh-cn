---
title: 内核模式安全整数函数摘要
description: 下表总结了可用于内核模式驱动程序的安全整数函数。
ms.assetid: 3DC016FA-5434-4581-9FBB-F6A8B54AB97B
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0d5e8754663f4fcbd05c7d50ae4b1c447bd1d9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836222"
---
# <a name="summary-of-kernel-mode-safe-integer-functions"></a>内核模式安全整数函数摘要


下表总结了可用于内核模式驱动程序的安全整数函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtldwordptradd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptradd" data-raw-source="[&lt;strong&gt;RtlDWordPtrAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptradd)"></a></a>RtlDWordPtrAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8add"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8add" data-raw-source="[&lt;strong&gt;RtlInt8Add&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8add)"></a></a>RtlInt8Add</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintadd" data-raw-source="[&lt;strong&gt;RtlIntAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintadd)"></a></a>RtlIntAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptradd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptradd" data-raw-source="[&lt;strong&gt;RtlIntPtrAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptradd)"></a></a>RtlIntPtrAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongadd" data-raw-source="[&lt;strong&gt;RtlLongLongAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongadd)"></a></a>RtlLongLongAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptradd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptradd" data-raw-source="[&lt;strong&gt;RtlLongPtrAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptradd)"></a></a>RtlLongPtrAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlptrdifftadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftadd" data-raw-source="[&lt;strong&gt;RtlPtrdiffTAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftadd)"></a></a>RtlPtrdiffTAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshortadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortadd" data-raw-source="[&lt;strong&gt;RtlShortAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortadd)"></a></a>RtlShortAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlsizetadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetadd" data-raw-source="[&lt;strong&gt;RtlSizeTAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetadd)"></a></a>RtlSizeTAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlssizetadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetadd" data-raw-source="[&lt;strong&gt;RtlSSIZETAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetadd)"></a></a>RtlSSIZETAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtluint8add"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8add" data-raw-source="[&lt;strong&gt;RtlUInt8Add&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8add)"></a></a>RtlUInt8Add</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintadd" data-raw-source="[&lt;strong&gt;RtlUIntAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintadd)"></a></a>RtlUIntAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptradd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptradd" data-raw-source="[&lt;strong&gt;RtlUIntPtrAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptradd)"></a></a>RtlUIntPtrAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongadd" data-raw-source="[&lt;strong&gt;RtlULongAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongadd)"></a></a>RtlULongAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongadd" data-raw-source="[&lt;strong&gt;RtlULongLongAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongadd)"></a></a>RtlULongLongAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptradd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptradd" data-raw-source="[&lt;strong&gt;RtlULongPtrAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptradd)"></a></a>RtlULongPtrAdd</dt>
<dd>
</dd>
<dt> <a href="" id="rtlushortadd"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortadd" data-raw-source="[&lt;strong&gt;RtlUShortAdd&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortadd)"></a></a>RtlUShortAdd</dt>
<dd>
</dd>
</dl></td>
<td><p>加法函数</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtldwordptrmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptrmult" data-raw-source="[&lt;strong&gt;RtlDWordPtrMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptrmult)"></a></a>RtlDWordPtrMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8mult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8mult" data-raw-source="[&lt;strong&gt;RtlInt8Mult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8mult)"></a></a>RtlInt8Mult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintmult" data-raw-source="[&lt;strong&gt;RtlIntMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintmult)"></a></a>RtlIntMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrmult" data-raw-source="[&lt;strong&gt;RtlIntPtrMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrmult)"></a></a>RtlIntPtrMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongmult" data-raw-source="[&lt;strong&gt;RtlLongLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongmult)"></a></a>RtlLongLongMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongmult" data-raw-source="[&lt;strong&gt;RtlLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongmult)"></a></a>RtlLongMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrmult" data-raw-source="[&lt;strong&gt;RtlLongPtrMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrmult)"></a></a>RtlLongPtrMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlptrdifftmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftmult" data-raw-source="[&lt;strong&gt;RtlPtrdiffTMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftmult)"></a></a>RtlPtrdiffTMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshortmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortmult" data-raw-source="[&lt;strong&gt;RtlShortMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortmult)"></a></a>RtlShortMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlssizetmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetmult" data-raw-source="[&lt;strong&gt;RtlSSIZETMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetmult)"></a></a>RtlSSIZETMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtluint8mult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8mult" data-raw-source="[&lt;strong&gt;RtlUInt8Mult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8mult)"></a></a>RtlUInt8Mult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlsizetmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetmult" data-raw-source="[&lt;strong&gt;RtlSizeTMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetmult)"></a></a>RtlSizeTMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlULongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)"></a></a>RtlULongMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongmult" data-raw-source="[&lt;strong&gt;RtlULongLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongmult)"></a></a>RtlULongLongMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrmult" data-raw-source="[&lt;strong&gt;RtlUIntPtrMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrmult)"></a></a>RtlUIntPtrMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintmult" data-raw-source="[&lt;strong&gt;RtlUIntMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintmult)"></a></a>RtlUIntMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrmult" data-raw-source="[&lt;strong&gt;RtlULongPtrMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrmult)"></a></a>RtlULongPtrMult</dt>
<dd>
</dd>
<dt> <a href="" id="rtlushortmult"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortmult" data-raw-source="[&lt;strong&gt;RtlUShortMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortmult)"></a></a>RtlUShortMult</dt>
<dd>
</dd>
</dl></td>
<td><p>乘法函数</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlshortsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortsub" data-raw-source="[&lt;strong&gt;RtlShortSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshortsub)"></a></a>RtlShortSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlushortsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortsub" data-raw-source="[&lt;strong&gt;RtlUShortSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushortsub)"></a></a>RtlUShortSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrsub" data-raw-source="[&lt;strong&gt;RtlULongPtrSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrsub)"></a></a>RtlULongPtrSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongsub" data-raw-source="[&lt;strong&gt;RtlULongLongSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongsub)"></a></a>RtlULongLongSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongsub" data-raw-source="[&lt;strong&gt;RtlULongSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongsub)"></a></a>RtlULongSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtluint8sub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8sub" data-raw-source="[&lt;strong&gt;RtlUInt8Sub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8sub)"></a></a>RtlUInt8Sub</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrsub" data-raw-source="[&lt;strong&gt;RtlUIntPtrSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrsub)"></a></a>RtlUIntPtrSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintsub" data-raw-source="[&lt;strong&gt;RtlUIntSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintsub)"></a></a>RtlUIntSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlssizetsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetsub" data-raw-source="[&lt;strong&gt;RtlSSIZETSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlssizetsub)"></a></a>RtlSSIZETSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlsizetsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetsub" data-raw-source="[&lt;strong&gt;RtlSizeTSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlsizetsub)"></a></a>RtlSizeTSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtldwordptrsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptrsub" data-raw-source="[&lt;strong&gt;RtlDWordPtrSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtldwordptrsub)"></a></a>RtlDWordPtrSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8sub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8sub" data-raw-source="[&lt;strong&gt;RtlInt8Sub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8sub)"></a></a>RtlInt8Sub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlptrdifftsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftsub" data-raw-source="[&lt;strong&gt;RtlPtrdiffTSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlptrdifftsub)"></a></a>RtlPtrdiffTSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongsub" data-raw-source="[&lt;strong&gt;RtlLongSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongsub)"></a></a>RtlLongSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintsub" data-raw-source="[&lt;strong&gt;RtlIntSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintsub)"></a></a>RtlIntSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongsub" data-raw-source="[&lt;strong&gt;RtlLongLongSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongsub)"></a></a>RtlLongLongSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrsub" data-raw-source="[&lt;strong&gt;RtlIntPtrSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrsub)"></a></a>RtlIntPtrSub</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrsub"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrsub" data-raw-source="[&lt;strong&gt;RtlLongPtrSub&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrsub)"></a></a>RtlLongPtrSub</dt>
<dd>
</dd>
</dl></td>
<td><p>减法函数</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlushorttoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttoshort" data-raw-source="[&lt;strong&gt;RtlUShortToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttoshort)"></a></a>RtlUShortToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoshort" data-raw-source="[&lt;strong&gt;RtlLongPtrToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoshort)"></a></a>RtlLongPtrToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoshort" data-raw-source="[&lt;strong&gt;RtlLongToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoshort)"></a></a>RtlLongToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoshort" data-raw-source="[&lt;strong&gt;RtlLongLongToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoshort)"></a></a>RtlLongLongToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoshort" data-raw-source="[&lt;strong&gt;RtlULongLongToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoshort)"></a></a>RtlULongLongToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoshort" data-raw-source="[&lt;strong&gt;RtlULongToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoshort)"></a></a>RtlULongToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoshort" data-raw-source="[&lt;strong&gt;RtlUIntPtrToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoshort)"></a></a>RtlUIntPtrToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoshort" data-raw-source="[&lt;strong&gt;RtlULongPtrToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoshort)"></a></a>RtlULongPtrToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoshort" data-raw-source="[&lt;strong&gt;RtlUIntToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoshort)"></a></a>RtlUIntToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoshort" data-raw-source="[&lt;strong&gt;RtlIntPtrToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoshort)"></a></a>RtlIntPtrToShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttoshort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoshort" data-raw-source="[&lt;strong&gt;RtlIntToShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoshort)"></a></a>RtlIntToShort</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Short</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtllongptrtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtochar" data-raw-source="[&lt;strong&gt;RtlLongPtrToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtochar)"></a></a>RtlLongPtrToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtochar" data-raw-source="[&lt;strong&gt;RtlLongLongToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtochar)"></a></a>RtlLongLongToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtluint8tochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8tochar" data-raw-source="[&lt;strong&gt;RtlUInt8ToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8tochar)"></a></a>RtlUInt8ToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtochar" data-raw-source="[&lt;strong&gt;RtlULongToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtochar)"></a></a>RtlULongToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtochar" data-raw-source="[&lt;strong&gt;RtlLongToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtochar)"></a></a>RtlLongToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtochar" data-raw-source="[&lt;strong&gt;RtlULongLongToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtochar)"></a></a>RtlULongLongToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttochar" data-raw-source="[&lt;strong&gt;RtlUIntToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttochar)"></a></a>RtlUIntToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttochar" data-raw-source="[&lt;strong&gt;RtlIntToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttochar)"></a></a>RtlIntToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtochar" data-raw-source="[&lt;strong&gt;RtlIntPtrToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtochar)"></a></a>RtlIntPtrToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtochar" data-raw-source="[&lt;strong&gt;RtlULongPtrToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtochar)"></a></a>RtlULongPtrToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttochar" data-raw-source="[&lt;strong&gt;RtlShortToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttochar)"></a></a>RtlShortToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlushorttochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttochar" data-raw-source="[&lt;strong&gt;RtlUShortToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttochar)"></a></a>RtlUShortToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlbytetochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlbytetochar" data-raw-source="[&lt;strong&gt;RtlByteToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlbytetochar)"></a></a>RtlByteToChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtochar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtochar" data-raw-source="[&lt;strong&gt;RtlUIntPtrToChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtochar)"></a></a>RtlUIntPtrToChar</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Char</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlintptrtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoint" data-raw-source="[&lt;strong&gt;RtlIntPtrToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoint)"></a></a>RtlIntPtrToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoint" data-raw-source="[&lt;strong&gt;RtlLongLongToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoint)"></a></a>RtlLongLongToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoint" data-raw-source="[&lt;strong&gt;RtlLongPtrToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoint)"></a></a>RtlLongPtrToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoint" data-raw-source="[&lt;strong&gt;RtlULongLongToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoint)"></a></a>RtlULongLongToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoint" data-raw-source="[&lt;strong&gt;RtlULongPtrToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoint)"></a></a>RtlULongPtrToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoint" data-raw-source="[&lt;strong&gt;RtlLongToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoint)"></a></a>RtlLongToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoint" data-raw-source="[&lt;strong&gt;RtlULongToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoint)"></a></a>RtlULongToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoint" data-raw-source="[&lt;strong&gt;RtlUIntToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoint)"></a></a>RtlUIntToInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtoint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint" data-raw-source="[&lt;strong&gt;RtlUIntPtrToInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint)"></a></a>RtlUIntPtrToInt</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Int</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtluint8toint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8toint8" data-raw-source="[&lt;strong&gt;RtlUInt8ToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluint8toint8)"></a></a>RtlUInt8ToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoint8" data-raw-source="[&lt;strong&gt;RtlLongLongToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoint8)"></a></a>RtlLongLongToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoint8" data-raw-source="[&lt;strong&gt;RtlLongPtrToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoint8)"></a></a>RtlLongPtrToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoint8" data-raw-source="[&lt;strong&gt;RtlULongPtrToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoint8)"></a></a>RtlULongPtrToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoint8" data-raw-source="[&lt;strong&gt;RtlLongToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoint8)"></a></a>RtlLongToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoint8" data-raw-source="[&lt;strong&gt;RtlULongLongToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoint8)"></a></a>RtlULongLongToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoint8" data-raw-source="[&lt;strong&gt;RtlULongToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoint8)"></a></a>RtlULongToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoint8" data-raw-source="[&lt;strong&gt;RtlIntToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoint8)"></a></a>RtlIntToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoint8" data-raw-source="[&lt;strong&gt;RtlIntPtrToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoint8)"></a></a>RtlIntPtrToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoint8" data-raw-source="[&lt;strong&gt;RtlUIntToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoint8)"></a></a>RtlUIntToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlbytetoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlbytetoint8" data-raw-source="[&lt;strong&gt;RtlByteToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlbytetoint8)"></a></a>RtlByteToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint8" data-raw-source="[&lt;strong&gt;RtlUIntPtrToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint8)"></a></a>RtlUIntPtrToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlushorttoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttoint8" data-raw-source="[&lt;strong&gt;RtlUShortToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttoint8)"></a></a>RtlUShortToInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttoint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoint8" data-raw-source="[&lt;strong&gt;RtlShortToInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoint8)"></a></a>RtlShortToInt8</dt>
<dd>
</dd>
</dl></td>
<td><p>转换到 Int8</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtluintptrtoint16"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint16" data-raw-source="[&lt;strong&gt;RtlUIntPtrToInt16&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint16)"></a></a>RtlUIntPtrToInt16</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Int16</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtllonglongtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtointptr" data-raw-source="[&lt;strong&gt;RtlLongLongToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtointptr)"></a></a>RtlLongLongToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtointptr" data-raw-source="[&lt;strong&gt;RtlLongPtrToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtointptr)"></a></a>RtlLongPtrToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtointptr" data-raw-source="[&lt;strong&gt;RtlLongToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtointptr)"></a></a>RtlLongToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtointptr" data-raw-source="[&lt;strong&gt;RtlULongToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtointptr)"></a></a>RtlULongToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtointptr" data-raw-source="[&lt;strong&gt;RtlULongPtrToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtointptr)"></a></a>RtlULongPtrToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtointptr" data-raw-source="[&lt;strong&gt;RtlUIntPtrToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtointptr)"></a></a>RtlUIntPtrToIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttointptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttointptr" data-raw-source="[&lt;strong&gt;RtlUIntToIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttointptr)"></a></a>RtlUIntToIntPtr</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 IntPtr</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlulongtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtolong" data-raw-source="[&lt;strong&gt;RtlULongToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtolong)"></a></a>RtlULongToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtolong" data-raw-source="[&lt;strong&gt;RtlIntPtrToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtolong)"></a></a>RtlIntPtrToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtolong" data-raw-source="[&lt;strong&gt;RtlLongLongToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtolong)"></a></a>RtlLongLongToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolong" data-raw-source="[&lt;strong&gt;RtlUIntPtrToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolong)"></a></a>RtlUIntPtrToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtolong" data-raw-source="[&lt;strong&gt;RtlLongPtrToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtolong)"></a></a>RtlLongPtrToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttolong" data-raw-source="[&lt;strong&gt;RtlUIntToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttolong)"></a></a>RtlUIntToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolong" data-raw-source="[&lt;strong&gt;RtlULongLongToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolong)"></a></a>RtlULongLongToLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtolong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolong" data-raw-source="[&lt;strong&gt;RtlULongPtrToLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolong)"></a></a>RtlULongPtrToLong</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Long</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlintptrtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtolongptr" data-raw-source="[&lt;strong&gt;RtlIntPtrToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtolongptr)"></a></a>RtlIntPtrToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtolongptr" data-raw-source="[&lt;strong&gt;RtlULongToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtolongptr)"></a></a>RtlULongToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtolongptr" data-raw-source="[&lt;strong&gt;RtlLongLongToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtolongptr)"></a></a>RtlLongLongToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolongptr" data-raw-source="[&lt;strong&gt;RtlUIntPtrToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolongptr)"></a></a>RtlUIntPtrToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolongptr" data-raw-source="[&lt;strong&gt;RtlULongLongToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolongptr)"></a></a>RtlULongLongToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttolongptr" data-raw-source="[&lt;strong&gt;RtlUIntToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttolongptr)"></a></a>RtlUIntToLongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtolongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolongptr" data-raw-source="[&lt;strong&gt;RtlULongPtrToLongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolongptr)"></a></a>RtlULongPtrToLongPtr</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 LongPtr</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlulonglongtolonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolonglong" data-raw-source="[&lt;strong&gt;RtlULongLongToLongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtolonglong)"></a></a>RtlULongLongToLongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtolonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolonglong" data-raw-source="[&lt;strong&gt;RtlULongPtrToLongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtolonglong)"></a></a>RtlULongPtrToLongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtolonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolonglong" data-raw-source="[&lt;strong&gt;RtlUIntPtrToLongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtolonglong)"></a></a>RtlUIntPtrToLongLong</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 LongLong</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlintptrtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoushort" data-raw-source="[&lt;strong&gt;RtlIntPtrToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoushort)"></a></a>RtlIntPtrToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8toushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toushort" data-raw-source="[&lt;strong&gt;RtlInt8ToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toushort)"></a></a>RtlInt8ToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoushort" data-raw-source="[&lt;strong&gt;RtlULongToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtoushort)"></a></a>RtlULongToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoushort" data-raw-source="[&lt;strong&gt;RtlIntToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoushort)"></a></a>RtlIntToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoushort" data-raw-source="[&lt;strong&gt;RtlLongLongToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoushort)"></a></a>RtlLongLongToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoushort" data-raw-source="[&lt;strong&gt;RtlLongPtrToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoushort)"></a></a>RtlLongPtrToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoushort" data-raw-source="[&lt;strong&gt;RtlLongToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoushort)"></a></a>RtlLongToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoushort" data-raw-source="[&lt;strong&gt;RtlShortToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoushort)"></a></a>RtlShortToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoushort" data-raw-source="[&lt;strong&gt;RtlUIntPtrToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoushort)"></a></a>RtlUIntPtrToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoushort" data-raw-source="[&lt;strong&gt;RtlUIntToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttoushort)"></a></a>RtlUIntToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoushort" data-raw-source="[&lt;strong&gt;RtlULongLongToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoushort)"></a></a>RtlULongLongToUShort</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtoushort"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoushort" data-raw-source="[&lt;strong&gt;RtlULongPtrToUShort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoushort)"></a></a>RtlULongPtrToUShort</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 UShort</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlushorttouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttouchar" data-raw-source="[&lt;strong&gt;RtlUShortToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttouchar)"></a></a>RtlUShortToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8touchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touchar" data-raw-source="[&lt;strong&gt;RtlInt8ToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touchar)"></a></a>RtlInt8ToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouchar" data-raw-source="[&lt;strong&gt;RtlIntPtrToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouchar)"></a></a>RtlIntPtrToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouchar" data-raw-source="[&lt;strong&gt;RtlIntToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouchar)"></a></a>RtlIntToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouchar" data-raw-source="[&lt;strong&gt;RtlLongLongToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouchar)"></a></a>RtlLongLongToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouchar" data-raw-source="[&lt;strong&gt;RtlLongPtrToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouchar)"></a></a>RtlLongPtrToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouchar" data-raw-source="[&lt;strong&gt;RtlLongToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouchar)"></a></a>RtlLongToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouchar" data-raw-source="[&lt;strong&gt;RtlShortToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouchar)"></a></a>RtlShortToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouchar" data-raw-source="[&lt;strong&gt;RtlUIntPtrToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouchar)"></a></a>RtlUIntPtrToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttouchar" data-raw-source="[&lt;strong&gt;RtlUIntToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttouchar)"></a></a>RtlUIntToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouchar" data-raw-source="[&lt;strong&gt;RtlULongLongToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouchar)"></a></a>RtlULongLongToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouchar" data-raw-source="[&lt;strong&gt;RtlULongPtrToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouchar)"></a></a>RtlULongPtrToUChar</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtouchar"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouchar" data-raw-source="[&lt;strong&gt;RtlULongToUChar&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouchar)"></a></a>RtlULongToUChar</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 UChar</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlint8touint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touint" data-raw-source="[&lt;strong&gt;RtlInt8ToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touint)"></a></a>RtlInt8ToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouint" data-raw-source="[&lt;strong&gt;RtlULongToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouint)"></a></a>RtlULongToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouint" data-raw-source="[&lt;strong&gt;RtlLongLongToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouint)"></a></a>RtlLongLongToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouint" data-raw-source="[&lt;strong&gt;RtlIntPtrToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouint)"></a></a>RtlIntPtrToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouint" data-raw-source="[&lt;strong&gt;RtlShortToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouint)"></a></a>RtlShortToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouint" data-raw-source="[&lt;strong&gt;RtlLongPtrToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouint)"></a></a>RtlLongPtrToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouint" data-raw-source="[&lt;strong&gt;RtlLongToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouint)"></a></a>RtlLongToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouint" data-raw-source="[&lt;strong&gt;RtlUIntPtrToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouint)"></a></a>RtlUIntPtrToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouint" data-raw-source="[&lt;strong&gt;RtlIntToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouint)"></a></a>RtlIntToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouint" data-raw-source="[&lt;strong&gt;RtlULongLongToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouint)"></a></a>RtlULongLongToUInt</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtouint"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouint" data-raw-source="[&lt;strong&gt;RtlULongPtrToUInt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouint)"></a></a>RtlULongPtrToUInt</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Uint</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlushorttouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttouint8" data-raw-source="[&lt;strong&gt;RtlUShortToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlushorttouint8)"></a></a>RtlUShortToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8touint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touint8" data-raw-source="[&lt;strong&gt;RtlInt8ToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touint8)"></a></a>RtlInt8ToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouint8" data-raw-source="[&lt;strong&gt;RtlLongLongToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtouint8)"></a></a>RtlLongLongToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouint8" data-raw-source="[&lt;strong&gt;RtlIntToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttouint8)"></a></a>RtlIntToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouint8" data-raw-source="[&lt;strong&gt;RtlIntPtrToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouint8)"></a></a>RtlIntPtrToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouint8" data-raw-source="[&lt;strong&gt;RtlLongPtrToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouint8)"></a></a>RtlLongPtrToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouint8" data-raw-source="[&lt;strong&gt;RtlShortToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouint8)"></a></a>RtlShortToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouint8" data-raw-source="[&lt;strong&gt;RtlLongToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouint8)"></a></a>RtlLongToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouint8" data-raw-source="[&lt;strong&gt;RtlUIntPtrToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtouint8)"></a></a>RtlUIntPtrToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtluinttouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttouint8" data-raw-source="[&lt;strong&gt;RtlUIntToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluinttouint8)"></a></a>RtlUIntToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouint8" data-raw-source="[&lt;strong&gt;RtlULongLongToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouint8)"></a></a>RtlULongLongToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouint8" data-raw-source="[&lt;strong&gt;RtlULongPtrToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouint8)"></a></a>RtlULongPtrToUInt8</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongtouint8"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouint8" data-raw-source="[&lt;strong&gt;RtlULongToUInt8&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouint8)"></a></a>RtlULongToUInt8</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Uint8</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtluintptrtouint16"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint16" data-raw-source="[&lt;strong&gt;RtlUIntPtrToUInt16&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoint16)"></a></a>RtlUIntPtrToUInt16</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 Uint16</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlulongtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouintptr" data-raw-source="[&lt;strong&gt;RtlULongToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongtouintptr)"></a></a>RtlULongToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouintptr" data-raw-source="[&lt;strong&gt;RtlLongToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtouintptr)"></a></a>RtlLongToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouintptr" data-raw-source="[&lt;strong&gt;RtlShortToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttouintptr)"></a></a>RtlShortToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8touintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touintptr" data-raw-source="[&lt;strong&gt;RtlInt8ToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8touintptr)"></a></a>RtlInt8ToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouintptr" data-raw-source="[&lt;strong&gt;RtlIntPtrToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtouintptr)"></a></a>RtlIntPtrToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouintptr" data-raw-source="[&lt;strong&gt;RtlLongPtrToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtouintptr)"></a></a>RtlLongPtrToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouintptr" data-raw-source="[&lt;strong&gt;RtlULongLongToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtouintptr)"></a></a>RtlULongLongToUIntPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulongptrtouintptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouintptr" data-raw-source="[&lt;strong&gt;RtlULongPtrToUIntPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtouintptr)"></a></a>RtlULongPtrToUIntPtr</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 UintPtr</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlulongptrtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoulong" data-raw-source="[&lt;strong&gt;RtlULongPtrToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongptrtoulong)"></a></a>RtlULongPtrToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8toulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulong" data-raw-source="[&lt;strong&gt;RtlInt8ToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulong)"></a></a>RtlInt8ToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulong" data-raw-source="[&lt;strong&gt;RtlIntPtrToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulong)"></a></a>RtlIntPtrToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoulong" data-raw-source="[&lt;strong&gt;RtlIntToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoulong)"></a></a>RtlIntToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoulong" data-raw-source="[&lt;strong&gt;RtlLongLongToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoulong)"></a></a>RtlLongLongToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulong" data-raw-source="[&lt;strong&gt;RtlLongPtrToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulong)"></a></a>RtlLongPtrToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulong" data-raw-source="[&lt;strong&gt;RtlLongToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulong)"></a></a>RtlLongToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulong" data-raw-source="[&lt;strong&gt;RtlShortToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulong)"></a></a>RtlShortToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtluintptrtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoulong" data-raw-source="[&lt;strong&gt;RtlUIntPtrToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtluintptrtoulong)"></a></a>RtlUIntPtrToULong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlulonglongtoulong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoulong" data-raw-source="[&lt;strong&gt;RtlULongLongToULong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoulong)"></a></a>RtlULongLongToULong</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 ULong</p></td>
</tr>
<tr class="even">
<td><p></p>
<dl>
<dt> <a href="" id="rtlshorttoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulonglong" data-raw-source="[&lt;strong&gt;RtlShortToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulonglong)"></a></a>RtlShortToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8toulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulonglong" data-raw-source="[&lt;strong&gt;RtlInt8ToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulonglong)"></a></a>RtlInt8ToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlinttoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoulonglong" data-raw-source="[&lt;strong&gt;RtlIntToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlinttoulonglong)"></a></a>RtlIntToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllonglongtoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoulonglong" data-raw-source="[&lt;strong&gt;RtlLongLongToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllonglongtoulonglong)"></a></a>RtlLongLongToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulonglong" data-raw-source="[&lt;strong&gt;RtlIntPtrToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulonglong)"></a></a>RtlIntPtrToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulonglong" data-raw-source="[&lt;strong&gt;RtlLongPtrToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulonglong)"></a></a>RtlLongPtrToULongLong</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoulonglong"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulonglong" data-raw-source="[&lt;strong&gt;RtlLongToULongLong&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulonglong)"></a></a>RtlLongToULongLong</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 ULongLong</p></td>
</tr>
<tr class="odd">
<td><p></p>
<dl>
<dt> <a href="" id="rtlulonglongtoulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoulongptr" data-raw-source="[&lt;strong&gt;RtlULongLongToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulonglongtoulongptr)"></a></a>RtlULongLongToULongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlintptrtoulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulongptr" data-raw-source="[&lt;strong&gt;RtlIntPtrToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlintptrtoulongptr)"></a></a>RtlIntPtrToULongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongptrtoulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulongptr" data-raw-source="[&lt;strong&gt;RtlLongPtrToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongptrtoulongptr)"></a></a>RtlLongPtrToULongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlint8toulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulongptr" data-raw-source="[&lt;strong&gt;RtlInt8ToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlint8toulongptr)"></a></a>RtlInt8ToULongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtllongtoulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulongptr" data-raw-source="[&lt;strong&gt;RtlLongToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtllongtoulongptr)"></a></a>RtlLongToULongPtr</dt>
<dd>
</dd>
<dt> <a href="" id="rtlshorttoulongptr"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulongptr" data-raw-source="[&lt;strong&gt;RtlShortToULongPtr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlshorttoulongptr)"></a></a>RtlShortToULongPtr</dt>
<dd>
</dd>
</dl></td>
<td><p>转换为 ULongPtr</p></td>
</tr>
</tbody>
</table>

 

 

 




