---
title: 支持的智能卡属性
description: 本主题介绍支持的智能卡属性。
ms.assetid: ''
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fbb292ea7c4e3e1bb5f60dc89d89b2e37e67dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373694"
---
# <a name="supported-smart-card-attributes"></a>支持的智能卡属性
本主题介绍当前支持的智能卡属性。 唯一受支持的属性如下所示;作为 STATUS_NOT_SUPPORTED 返回 Winsmcrd.h 中定义的所有其他属性。 中说明了这些属性*ICCs 和个人计算机系统的互操作性规范*。

<table>
    <tbody>
        <tr>
            <th>属性标记</th>
            <th>描述</th>
        </tr>
        <tr>
            <td>CARD_ATTR_CURRENT_PROTOCOL_TYPE</td>
            <td>SCARD_PROTOCOL_T1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_CLK</td>
            <td>13560 （13.56 MHz 的小字节序整数）</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_D</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_IFSC</td>
            <td>32</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_IFSD</td>
            <td>254</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CURRENT_BWT</td>
            <td>4</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEFAULT_CLK</td>
            <td>13560</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_CLK</td>
            <td>13560</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEFAULT_DATA_RATE</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_DATA_RATE</td>
            <td>1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CHARACTERISTICS</td>
            <td>SCARD_READER_CONTACTLESS</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_MAX_IFSD</td>
            <td>254</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_NAME</td>
            <td>ASCII 字符串</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_IFD_TYPE</td>
            <td>ASCII 字符串</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_VENDOR_IFD_VERSION</td>
            <td>0x01000010，版本 1.0.0.1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_PROTOCOL_TYPES</td>
            <td>SCARD_PROTOCOL_T1</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_DEVICE_UNIT</td>
            <td>0</td>
        </tr>
        <tr>
            <td>SCARD_ATTR_CHANNEL_ID</td>
            <td>
双字节编码为 0xDDDDCCCC，其中 DDDD 是数据通道类型，CCCC 是频道号。 为 DDDD 定义以下编码： <table>
                    <tbody>
                        <tr>
                            <th>数据通道 (DDDD)</th>
                            <th>在任务栏的搜索框中键入</th>
                            <th>频道号 (CCCC)</th>
                        </tr>
                        <tr>
                            <td>0x0100</td>
                            <td>NFC</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0x0200</td>
                            <td>UICC</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0x0800</td>
                            <td>嵌入的 SE</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>0xFXXX</td>
                            <td>供应商定义的通道类型</td>
                            <td>供应商定义</td>
                        </tr><br/>                    </tbody>
                </table>
            </td>
        </tr>
    <tbody>
</table>

## <a name="icc-attributes"></a>ICC 属性

<table>
    <tbody>
        <tr>
            <th>属性标记</th>
            <th>描述</th>
        </tr>
        <tr>
            <td>SCARD_ATTR_ICC_PRESENCE</td>
            <td>（1 个字节） <ul>
                    <li> 0 = 不存在 </li>
                    <li> 1 = 存在的卡</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>SCARD_ATTR_ATR_STRING</td>
            <td>（32 字节） <ul>
                    <li> ATR 字符串 </li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>SCARD_ATTR_ICC_TYPE_PER_ATR</td>
            <td>（1 个字节） <ul>
                    <li> 0 = 未知的类型 </li>
                    <li> 5 = 14443A </li>
                    <li> 6 = 14443B </li>
                    <li> 7 = ISO-15693 </li>
                </ul>
            </td>
        </tr>
