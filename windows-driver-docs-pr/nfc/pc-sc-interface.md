---
title: 智能卡的 PC/SC 接口
description: 本主题介绍不同的 NFC 卡类型的 ATR 格式。
ms.assetid: ''
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb96aa0d8dd80f0a478a9512b1eaef9e9a9b3ebf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543626"
---
# <a name="pcsc-interface-for-smart-cards"></a>智能卡的 PC/SC 接口

下面列出了不同的 NFC 卡类型的 ATR 格式。 请参阅有关 ATR 格式的更多详细信息的 PC/SC 规范 [3.a]。

## <a name="atr-format-for-iso14443-4-cards"></a>ISO14443 4 卡的 ATR 格式

| 字节偏移量 | 值 | 指定内容      | 描述                                                                                                                 |
|-------------|-------|------------------|-----------------------------------------------------------------------------------------------------------------------------|
| 0           | 3B    | 初始标头   |                                                                                                                             |
| 1           | 8n    | T0               | 更高版本的四位指示仅存在 TD1。 较低的位元组表示历史字节的大小                       |
| 2           | 80    | TD1              | 存在 TD2                                                                                                             |
| 3           | 01    | TD2              |                                                                                                                             |
| 4 到 3 + N    | XX    | 历史的字节数 | 有关 ISO14443A:历史的字节数是从 ATS 响应 <br> 有关 ISO14443B:历史的字节数是从 ATTRIB (ATQB) |
| 4+N         | XX    | TCK              | 校验和                                                                                                                    |

## <a name="atr-format-for-storage-cards"></a>存储卡的 ATR 格式
<table>
    <tbody>
        <tr>
            <th>字节偏移量</th>
            <th>值</th>
            <th>指定内容</th>
            <th>描述</th>
        </tr>
        <tr>
            <td>0</td>
            <td>3B</td>
            <td>初始标头</td>
        </tr>
        <tr>
            <td>1</td>
            <td>8n</td>
            <td>T0</td>
            <td>更高版本的四位指示仅存在 TD1。 较低的位元组表示历史字节的大小。</td>
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
            <td>4 到 3 + N</td>
            <td>80</td>
            <td>T1</td>
            <td>类别指示器字节。</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>4F</td>
            <td>TK</td>
            <td>应用程序标识符存在。</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>0C</td>
            <td>TK</td>
            <td>长度</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>A0 00 00 03 06</td>
            <td>TK</td>
            <td>指定在第 3 部分补充文档从 PC/SC 中 RID</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>SS</td>
            <td>TK</td>
            <td>对于标准的字节。 值应对应于表 2 的补充文档。</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>NN</td>
            <td>TK</td>
            <td>卡名称的字节数。 值应对应于表 3 的补充文档。</td>
        </tr>
        <tr>
            <td>4 到 3 + N</td>
            <td>00 00 00 00</td>
            <td>RFU</td>
            <td></td>
        </tr>
        <tr>
            <td>4+N</td>
            <td>XX</td>
            <td>TCK<td>
            <td>校验和</td>
        </tr>
    </tbody>
</table>
