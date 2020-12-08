---
title: 适用于智能卡的 PC/SC 接口
description: 本主题介绍不同 NFC 卡类型的 ATR 格式。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d253b1e85706cfcc5bddc9f31245741c9b75a922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812773"
---
# <a name="pcsc-interface-for-smart-cards"></a>适用于智能卡的 PC/SC 接口

下面列出了不同 NFC 卡类型的 ATR 格式。 有关 ATR 格式的更多详细信息，请参阅 PC/SC spec [3. a]。

## <a name="atr-format-for-iso14443-4-cards"></a>ISO14443 的 ATR 格式-4 卡

| 字节偏移量 | “值” | 职务      | 描述                                                                                                                 |
|-------------|-------|------------------|-----------------------------------------------------------------------------------------------------------------------------|
| 0           | 3B    | 初始标头   |                                                                                                                             |
| 1           | 1uk-8n-qpp    | T0               | 较大的半字节表明仅存在 TD1。 下半半部分指示历史字节的大小                       |
| 2           | 80    | TD1              | 存在 TD2                                                                                                             |
| 3           | 01    | TD2              |                                                                                                                             |
| 4到 3 + N    | XX    | 历史字节数 | 对于 ISO14443A：历史字节来自 ATS 响应 <br> 对于 ISO14443B：历史字节来自 ATTRIB (ATQB)  |
| 4 + N         | XX    | TCK              | 校验和                                                                                                                    |

## <a name="atr-format-for-storage-cards"></a>存储卡的 ATR 格式
<table>
    <tbody>
        <tr>
            <th>字节偏移量</th>
            <th>“值”</th>
            <th>职务</th>
            <th>描述</th>
        </tr>
        <tr>
            <td>0</td>
            <td>3B</td>
            <td>初始标头</td>
        </tr>
        <tr>
            <td>1</td>
            <td>1uk-8n-qpp</td>
            <td>T0</td>
            <td>较大的半字节表明仅存在 TD1。 下半半部分指示历史字节的大小。</td>
        </tr>
        <tr>
            <td>2</td>
            <td>80</td>
            <td>TD1</td>
            <td>存在 TD2</td>
        </tr>
        <tr>
            <td>3</td>
            <td>01</td>
            <td>TD2</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>80</td>
            <td>T1</td>
            <td>类别指示器字节。</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>4F</td>
            <td>TK</td>
            <td>应用程序标识符存在。</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>0C</td>
            <td>TK</td>
            <td>长度</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>A0 00 00 03 06</td>
            <td>TK</td>
            <td>从 PC/SC 的第3部分补充文档中指定的 RID</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>SS</td>
            <td>TK</td>
            <td>标准字节。 值应对应于补充文档的表2。</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>NN</td>
            <td>TK</td>
            <td>卡名称的字节数。 值应对应于补充文档的表3。</td>
        </tr>
        <tr>
            <td>4到 3 + N</td>
            <td>00 00 00 00</td>
            <td>RFU</td>
            <td></td>
        </tr>
        <tr>
            <td>4 + N</td>
            <td>XX</td>
            <td>TCK<td>
            <td>检查-sum</td>
        </tr>
    </tbody>
</table>
