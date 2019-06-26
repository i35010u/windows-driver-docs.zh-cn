---
title: MagneticStripeReaderDataReceived
description: MagneticStripeReaderDataReceived 事件引发后的成功磁条阅读器 (MSR) 扫描事件。
ms.assetid: 5074669c-3914-4d15-983b-d979c7f88b21
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2bc54dbb622efcc825566822ad88687b07a423d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363381"
---
# <a name="magneticstripereaderdatareceived"></a>MagneticStripeReaderDataReceived

成功磁条阅读器 (MSR) 扫描事件后，引发此事件。

## <a name="syntax"></a>语法

```cpp
typedef struct _MSR_DATA_RECEIVED {
    MsrCardType CardType;
    unsigned char Track1EncryptedDataLength;
    unsigned char Track2EncryptedDataLength;
    unsigned char Track3EncryptedDataLength;
    unsigned char Track4EncryptedDataLength;
    unsigned char Track1EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track2EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track3EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track4EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track1MaskedDataLength;
    unsigned char Track2MaskedDataLength;
    unsigned char Track3MaskedDataLength;
    unsigned char Track4MaskedDataLength;
    unsigned char Track1MaskedData[MSR_TRACK_SIZE];
    unsigned char Track2MaskedData[MSR_TRACK_SIZE];
    unsigned char Track3MaskedData[MSR_TRACK_SIZE];
    unsigned char Track4MaskedData[MSR_TRACK_SIZE];
    unsigned char Track1DiscretionaryDataLength;
    unsigned char Track2DiscretionaryDataLength;
    unsigned char Track1DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char Track2DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char CardAuthenicationDataLength; // Length of data after encryption, may include padding.
    unsigned char CardAuthenticationDataAbsoluteLength; // Length of data before encryption, may be needed to strip padding on decryption.
    unsigned char CardAuthenicationData[MSR_CARD_AUTHENTICATION_DATA_SIZE];
    unsigned char AdditionalSecurityInformationLength;
    unsigned char AdditionalSecurityInformation[MSR_ADDITIONAL_SECURITY_INFORMATION_SIZE];
} MSR_DATA_RECEIVED, *PMSR_DATA_RECEIVED;
```

下表显示了此事件的数据缓冲区的内存布局。

| 内存值 | 描述 
|---|---|
| 0x00000008                                                          | **事件类型 = PosEventType::MagneticStripeReaderDataReceived**                                                                       |
| UINT32                                                              | **DataLength** = sizeof(**PosEventDataHeader**) + sizeof(**MSR\_DATA\_RECEIVED**)                                                     |
| 32-bit MsrCardType                                                  | [MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                                                                                                        |
| 无符号字符型                                                       | **Track1EncryptedDataLength** -将始终为零 (0)，如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)是**MsrDataEncryption\_None**。 |
| 无符号字符型                                                       | **Track2EncryptedDataLength** -将始终为零 (0)，如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)是**MsrDataEncryption\_None**。 |
| 无符号字符型                                                       | **Track3EncryptedDataLength** -将始终为零 (0)，如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)是**MsrDataEncryption\_None**。 |
| 无符号字符型                                                       | **Track4EncryptedDataLength** -将始终为零 (0)，如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)是**MsrDataEncryption\_None**。 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1EncryptedDataLength**加密的跟踪 1 数据的字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2EncryptedDataLength**加密的跟踪 2 数据的字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3EncryptedDataLength**加密的跟踪 3 数据的字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4EncryptedDataLength**加密的跟踪 4 数据的字节                                                                         |
| 无符号字符型                                                       | **Track1MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track2MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track3MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track4MaskedDataLength**                                                                                                            |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1MaskedDataLength**字节的掩码跟踪 1 个数据                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2MaskedDataLength**字节的掩码跟踪 2 数据                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3MaskedDataLength**字节的掩码跟踪 3 个数据                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4MaskedDataLength**字节的掩码跟踪 4 数据                                                                               |
| 无符号字符型                                                       | **Track1DiscretionaryDataLength** – 将始终为零 (0)，如果**MagneticStripeReaderIsDecodeDataEnabled**为 false。                |
| 无符号字符型                                                       | **Track2DiscretionaryDataLength**– 将始终为零 (0)，如果**MagneticStripeReaderIsDecodeDataEnabled**为 false。                 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1DiscretionaryDataLength**字节的自定义跟踪 1 个数据                                                                 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2DiscretionaryDataLength**字节的自定义跟踪 2 数据                                                                 |
| 无符号字符型                                                       | **CardAuthenicationDataLength** -长度以字节为单位，包括填充的加密数据                                            |
| 无符号字符型                                                       | **CardAuthenticationDataAbsoluteLength** -长度以字节为单位 （您可能需要去除解密期间填充） 未加密的数据  |
| 无符号 char\[MSR\_其他\_安全\_信息\_数据\_大小\] | **CardAuthenticationDataAbsoluteLength**卡身份验证数据的字节数                                                            |
| 无符号字符型                                                       | **AdditionalSecurityInformationLength**                                                                                               |
| 无符号 char\[MSR\_其他\_安全\_信息\_大小\]       | **AdditionalSecurityInformationLength**字节的额外的安全信息                                                      |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
