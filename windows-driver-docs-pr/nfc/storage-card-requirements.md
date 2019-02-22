---
title: 存储卡的要求
description: 本主题介绍存储卡 APDU 要求
ms.assetid: ''
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3b18621098a4a28084b8d8a54b3098a23e2595cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546482"
---
# <a name="storage-card-requirements"></a>存储卡的要求

本部分介绍非 ISO14443 4 兼容的卡 （称为存储卡） 的一般 APDU 命令集要求。

## <a name="general-authenticate-command"></a>常规进行身份验证的命令

常规进行身份验证命令用于执行身份验证的一系列 MIFARE 卡上。 此命令当前仅适用于 MIFARE Mini、 经典 1 k 和 4 k 卡。 

### <a name="command-format"></a>命令格式

| 命令              | 类 | INS  | P1   | P2   | Lc   | 中的数据                                               |
|----------------------|-------|------|------|------|------|-------------------------------------------------------|
| General-Authenticate | 0xFF  | 0x86 | 0x00 | 0x00 | 0x01 | 地址 MSB，地址 LSB，密钥类型 A 或 B，键数字 |

### <a name="response-format"></a>响应格式

| 响应 |
|----------|
| SW1, SW2  |

## <a name="get-data-command"></a>获取数据命令

获取数据命令用于从非接触式的 NFC 标记/智能卡中检索信息。 

### <a name="command-format"></a>命令格式

<table>
    <tbody>
        <tr>
            <th>命令</th>
            <th>类</th>
            <th>INS</th>
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
                    <li>0x00:卡 （a: ISO14443 的序列号UID，ISO14443 B:PUPI，Felica:IDm，包装盒：RID)</li>
                    <li>0x01:历史字节的卡 （类型 a:历史个字节从 ATR，类型 b:ATTRIB 响应）</li>
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
| 输出数据量 SW1，SW2 |

## <a name="load-key-command"></a>负载 Key 命令

负载 Key 命令用于将 MIFARE 密钥存储在驱动程序。 此命令当前仅适用于 MIFARE Mini、 经典 1 k 和 4 k 卡。 

### <a name="command-format"></a>命令格式

| 命令  | 类 | INS  | P1            | P2         | Lc  | 中的数据   |
|----------|-------|------|---------------|------------|-----|-----------|
| 加载密钥 | 0xFF  | 0x82 | 键结构 | 密钥号 | 0x6 | 密钥值 |

### <a name="response-format"></a>响应格式

| 响应 |
|----------|
| SW1, SW2 |

## <a name="manage-session-command"></a>管理会话命令

此命令的实现应按 PCSC 规范。

### <a name="command-format"></a>命令格式

| 命令              | 类 | INS  | P1   | P2   | Lc       | 中的数据         |
|----------------------|-------|------|------|------|----------|-----------------|
| 常规身份验证 | 0xFF  | 0xC2 | 0x00 | 0x00 | 变量 | TLV 数据对象 |

以下是所需的 TLV 数据对象来驱动程序支持：

| Tag  | 数据对象               |
|------|---------------------------|
| 0x80 | 版本数据对象       |
| 0x81 | 启动透明会话 |
| 0x82 | 结束透明会话   |

## <a name="read-binary-command"></a>读取二进制命令

读取二进制命令用于从非接触式的 NFC 标记/智能卡中读取数据。 命令为仅适用于存储卡 （卡 MIFARE 经典/u L、 Felica、 ISO15693 和包装盒/简称 Topaz）。

### <a name="command-format"></a>命令格式

| 命令     | 类 | INS  | P1          | P2          | Lc                | 中的数据 | Li              |
|-------------|-------|------|-------------|-------------|-------------------|---------|-----------------|
| 读取二进制文件 | 0xFF  | 0xB0 | 地址 MSB | 地址 LSB | 中的数据的长度 | 数据    | 预期的长度 |

### <a name="mifare-family"></a>MIFARE 系列

| 命令       | CLA  | INS  | P1   | P2           | le   |
|---------------|------|------|------|--------------|------|
| UL 读取 16    | 0xFF | 0xB0 | 0x00 | 0x00 到 0x15 | 0x10 |
| CL 1 k 读取 16 | 0xFF | 0xB0 | 0x00 | 0x00 到 0x3F | 0x10 |
| CL 4k READ 16 | 0xFF | 0xB0 | 0x00 | 0x00 到 0xFF | 0x10 |

### <a name="jewel-family"></a>包装盒系列

| 命令  | CLA  | INS  | P1       | P2           | le   |
|----------|------|------|----------|--------------|------|
| 读取所有 | 0xFF | 0xB0 | 0x00     | 0x00         | 0x00 |
| RID      | 0xFF | 0xB0 | 0x00     | 0x00         | 0x06 |
| 读取     | 0xFF | 0xB0 | 块否 | 块偏移量 | 0x01 |
| 读取 8   | 0xFF | 0xB0 | 块否 | 0x00         | 0x08 |
| 读取 SEG | 0xFF | 0xB0 | 0x00     | 段 Addr | 0x80 |

### <a name="felica-family"></a>Felica 系列

| 命令 | CLA  | INS  | P1   | P2   | Lc                | 中的数据                                         |
|---------|------|------|------|------|-------------------|-------------------------------------------------|
| 检查   | 0xFF | 0xB0 | 0x00 | 0x00 | 中的数据的长度 | 大量服务，数量的块，块列表 |

### <a name="iso-15693-family"></a>ISO 15693 系列

| 命令 | CLA  | INS  | P1           | P2   | le   |
|---------|------|------|--------------|------|------|
| 读取    | 0xFF | 0xB0 | 块号 | 0x00 | 0x04 |

### <a name="response"></a>响应

| 响应           |
|--------------------|
| 输出数据量 SW1，SW2 |

## <a name="transparent-exchange-command"></a>透明 exchange 命令

### <a name="command-format"></a>命令格式

| 命令              | 类 | INS  | P1   | P2   | Lc       | 中的数据         |
|----------------------|-------|------|------|------|----------|-----------------|
| 常规身份验证 | 0xFF  | 0xC2 | 0x00 | 0x01 | 变量 | TLV 数据对象 | 

以下是透明的 Exchange 命令必须由透明 exchange 命令传输到存储卡的驱动程序支持所需的 TLV 数据对象：

| Tag    | 数据对象                       |
|--------|-----------------------------------|
| 0x95   | 收发的传输和接收 |
| 0x5F46 | 计时器                             |

## <a name="update-binary-command"></a>更新二进制文件命令

更新二进制文件命令用于将数据写入到非接触式 NFC 标记/卡。 命令为仅适用于存储卡 （卡 MIFARE 经典/u L、 Felica、 ISO15693 和包装盒/简称 Topaz）。 请求和响应命令的格式为如下所述。

### <a name="command-format"></a>命令格式

| 命令       | 类 | INS  | P1          | P2          | Lc                | 中的数据 |
|---------------|-------|------|-------------|-------------|-------------------|---------|
| 更新二进制文件 | 0xFF  | 0xD6 | 地址 MSB | 地址 LSB | 中的数据的长度 | 数据    |

### <a name="mifare-family"></a>MIFARE 系列

| 命令        | CLA  | INS  | P1   | P2           | le   |
|----------------|------|------|------|--------------|------|
| UL 写 4     | 0xFF | 0xD6 | 0x00 | 0x00 到 0x15 | 0x04 |
| CL 1 k 写 16 | 0xFF | 0xD6 | 0x00 | 0x00 到 0x3F | 0x10 |
| CL 4k 写入 16 | 0xFF | 0xB0 | 0x00 | 0x00 到 0xFF | 0x10 |

### <a name="jewel-family"></a>包装盒系列

| 命令  | CLA  | INS  | P1           | P2           | le   |
|----------|------|------|--------------|--------------|------|
| WRITE1-E | 0xFF | 0xD6 | 块号 | 块偏移量 | 0x01 |
| WRITE8-E | 0xFF | 0xD6 | 块号 | 0x00         | 0x08 |

### <a name="felica-family"></a>Felica 系列

| 命令 | CLA  | INS  | P1   | P2   | le                | 中的数据                                         |
|---------|------|------|------|------|-------------------|-------------------------------------------------|
| 更新  | 0xFF | 0xD6 | 0x00 | 0x00 | 中的数据的长度 | 大量服务，块，块列表数目 |

### <a name="response-format"></a>响应格式

| 命令 | CLA  | INS  | P1           | P2   | le  |
|---------|------|------|--------------|------|-----|
| 编写   | 0xFF | 0xD6 | 块号 | 0x00 | 0x4 |

