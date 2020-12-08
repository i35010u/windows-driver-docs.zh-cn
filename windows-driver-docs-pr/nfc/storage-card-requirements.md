---
title: 存储卡要求
description: 本主题介绍存储卡的 APDU 要求
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aebd0ab19c72fd25fdc63cc27c5c8cc14b6f6058
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812705"
---
# <a name="storage-card-requirements"></a>存储卡要求

本部分介绍了对非 ISO14443 兼容卡 (称为存储卡) 的常规 APDU 命令集要求。

## <a name="general-authenticate-command"></a>General-Authenticate 命令

General-Authenticate 命令用于在 MIFARE 卡上执行身份验证序列。 此命令仅适用于 MIFARE 微型、经典1k 和4k 卡。 

### <a name="command-format"></a>命令格式

| 命令              | 类 | Ins  | P1   | P2   | Lc-fc   | 数据输入                                               |
|----------------------|-------|------|------|------|------|-------------------------------------------------------|
| General-Authenticate | 0xFF  | 0x86 | 0x00 | 0x00 | 0x01 | Address MSB，Address LSB，Key Type A 或 B，Key Number |

### <a name="response-format"></a>响应格式

| 响应 |
|----------|
| SW1, SW2  |

## <a name="get-data-command"></a>Get-Data 命令

Get-Data 命令用于从 contactless NFC 标记/卡中检索信息。 

### <a name="command-format"></a>命令格式

<table>
    <tbody>
        <tr>
            <th>命令</th>
            <th>类</th>
            <th>Ins</th>
            <th>P1</th>
            <th>P2</th>
            <th>L2</th>
        </tr>
        <tr>
            <td>Get-Data</td>
            <td>0xFF</td>
            <td>0xCA</td>
            <td>
                <ul>
                    <li>0x00：卡的序列号 (ISO14443： UID，ISO14443-B： PUPI，Felica： IDm，宝石： RID) </li>
                    <li>0x01：卡的历史字节 (键入 A： ATR 的历史字节，类型 B： ATTRIB response) </li>
                </ul>
            </td>
            <td>0x00</td>
            <td>0x00</td>
        </tr>
    <tbody>
</table>

### <a name="response-format"></a>响应格式

| 响应           |
|--------------------|
| 数据输出，SW1，SW2 |

## <a name="load-key-command"></a>Load-Key 命令

Load-Key 命令用于将 MIFARE 密钥存储在驱动程序中。 此命令仅适用于 MIFARE 微型、经典1k 和4k 卡。 

### <a name="command-format"></a>命令格式

| 命令  | 类 | Ins  | P1            | P2         | Lc-fc  | 数据输入   |
|----------|-------|------|---------------|------------|-----|-----------|
| Load-Key | 0xFF  | 0x82 | 键结构 | 密钥号 | 0x6 | 键值 |

### <a name="response-format"></a>响应格式

| 响应 |
|----------|
| SW1, SW2 |

## <a name="manage-session-command"></a>管理会话命令

此命令的实现应按照 PCSC 规范进行。

### <a name="command-format"></a>命令格式

| 命令              | 类 | Ins  | P1   | P2   | Lc-fc       | 数据输入         |
|----------------------|-------|------|------|------|----------|-----------------|
| 一般身份验证 | 0xFF  | 0xC2 | 0x00 | 0x00 | 变量 | TLV 数据对象 |

下面是驱动程序支持的必需 TLV 数据对象：

| 标记  | 数据对象               |
|------|---------------------------|
| 0x80 | 版本数据对象       |
| 0x81 | 启动透明会话 |
| 0x82 | 结束透明会话   |

## <a name="read-binary-command"></a>Read-Binary 命令

Read-Binary 命令用于从 contactless NFC 标记/卡读取数据。 命令仅适用于 (MIFARE 经典/UL、Felica、ISO15693 和后) 的存储卡。

### <a name="command-format"></a>命令格式

| 命令     | 类 | Ins  | P1          | P2          | Lc-fc                | 数据输入 | Li              |
|-------------|-------|------|-------------|-------------|-------------------|---------|-----------------|
| Read-Binary | 0xFF  | 0xB0 | 地址 MSB | 地址 LSB | 数据的长度 | 数据    | 应为长度 |

### <a name="mifare-family"></a>MIFARE 系列

| 命令       | CLA  | Ins  | P1   | P2           | Le   |
|---------------|------|------|------|--------------|------|
| UL 读取16    | 0xFF | 0xB0 | 0x00 | 0x00 到0x15 | 0x10 |
| CL 1k READ 16 | 0xFF | 0xB0 | 0x00 | 0x00 到0x3F | 0x10 |
| CL 4k 读取16 | 0xFF | 0xB0 | 0x00 | 0x00 到0xFF | 0x10 |

### <a name="jewel-family"></a>宝石系列

| 命令  | CLA  | Ins  | P1       | P2           | Le   |
|----------|------|------|----------|--------------|------|
| 全部读取 | 0xFF | 0xB0 | 0x00     | 0x00         | 0x00 |
| RID      | 0xFF | 0xB0 | 0x00     | 0x00         | 0x06 |
| READ     | 0xFF | 0xB0 | 禁止 | 块偏移量 | 0x01 |
| 读取8   | 0xFF | 0xB0 | 禁止 | 0x00         | 0x08 |
| 读取 SEG | 0xFF | 0xB0 | 0x00     | 段地址 | 0x80 |

### <a name="felica-family"></a>Felica 系列

| 命令 | CLA  | Ins  | P1   | P2   | Lc-fc                | 数据输入                                         |
|---------|------|------|------|------|-------------------|-------------------------------------------------|
| CHECK   | 0xFF | 0xB0 | 0x00 | 0x00 | 数据的长度 | 服务数量、块数、块列表 |

### <a name="iso-15693-family"></a>ISO 15693 系列

| 命令 | CLA  | Ins  | P1           | P2   | Le   |
|---------|------|------|--------------|------|------|
| READ    | 0xFF | 0xB0 | 块号 | 0x00 | 0x04 |

### <a name="response"></a>响应

| 响应           |
|--------------------|
| 数据输出，SW1，SW2 |

## <a name="transparent-exchange-command"></a>透明交换命令

### <a name="command-format"></a>命令格式

| 命令              | 类 | Ins  | P1   | P2   | Lc-fc       | 数据输入         |
|----------------------|-------|------|------|------|----------|-----------------|
| 一般身份验证 | 0xFF  | 0xC2 | 0x00 | 0x01 | 变量 | TLV 数据对象 | 

下面是用于透明交换命令的必需 TLV 数据对象，这些对象可由驱动程序支持，以便透明地将命令交换到存储卡：

| 标记    | 数据对象                       |
|--------|-----------------------------------|
| 0x95   | Transceive-传输和接收 |
| 0x5F46 | 计时器                             |

## <a name="update-binary-command"></a>Update-Binary 命令

Update-Binary 命令用于将数据写入 contactless NFC 标记/卡。 命令仅适用于 (MIFARE 经典/UL、Felica、ISO15693 和后) 的存储卡。 命令的请求和响应的格式如下所述。

### <a name="command-format"></a>命令格式

| 命令       | 类 | Ins  | P1          | P2          | Lc-fc                | 数据输入 |
|---------------|-------|------|-------------|-------------|-------------------|---------|
| Update-Binary | 0xFF  | 0xD6 | 地址 MSB | 地址 LSB | 数据的长度 | 数据    |

### <a name="mifare-family"></a>MIFARE 系列

| 命令        | CLA  | Ins  | P1   | P2           | Le   |
|----------------|------|------|------|--------------|------|
| UL 写入4     | 0xFF | 0xD6 | 0x00 | 0x00 到0x15 | 0x04 |
| CL 1k 写入16 | 0xFF | 0xD6 | 0x00 | 0x00 到0x3F | 0x10 |
| CL 4k 写入16 | 0xFF | 0xB0 | 0x00 | 0x00 到0xFF | 0x10 |

### <a name="jewel-family"></a>宝石系列

| 命令  | CLA  | Ins  | P1           | P2           | Le   |
|----------|------|------|--------------|--------------|------|
| WRITE1-E | 0xFF | 0xD6 | 块号 | 块偏移量 | 0x01 |
| WRITE8-E | 0xFF | 0xD6 | 块号 | 0x00         | 0x08 |

### <a name="felica-family"></a>Felica 系列

| 命令 | CLA  | Ins  | P1   | P2   | Le                | 数据输入                                         |
|---------|------|------|------|------|-------------------|-------------------------------------------------|
| UPDATE  | 0xFF | 0xD6 | 0x00 | 0x00 | 数据的长度 | 服务数量、块数、块列表 |

### <a name="response-format"></a>响应格式

| 命令 | CLA  | Ins  | P1           | P2   | Le  |
|---------|------|------|--------------|------|-----|
| WRITE   | 0xFF | 0xD6 | 块号 | 0x00 | 0x4 |

