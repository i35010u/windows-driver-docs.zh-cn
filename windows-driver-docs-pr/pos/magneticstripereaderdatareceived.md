---
title: MagneticStripeReaderDataReceived
description: 成功的磁条读取器（MSR）扫描事件之后，将引发 MagneticStripeReaderDataReceived 事件。
ms.assetid: 5074669c-3914-4d15-983b-d979c7f88b21
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c82de8f8149b208fb8d26cad7101e8617ca5770
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843573"
---
# <a name="magneticstripereaderdatareceived"></a>MagneticStripeReaderDataReceived

成功的磁条读取器（MSR）扫描事件后引发此事件。

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

下表显示此事件的数据缓冲区的内存布局。

| 内存值 | 描述 
|---|---|
| 0x00000008                                                          | **事件 = PosEventType：： MagneticStripeReaderDataReceived**                                                                       |
| UINT32                                                              | **DataLength** = Sizeof （**PosEventDataHeader**） + sizeof （**MSR\_\_接收的数据**）                                                     |
| 32位 MsrCardType                                                  | [MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                                                                                                        |
| 无符号字符型                                                       | **Track1EncryptedDataLength** -如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)为**MsrDataEncryption\_None**，将始终为零（0）。 |
| 无符号字符型                                                       | **Track2EncryptedDataLength** -如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)为**MsrDataEncryption\_None**，将始终为零（0）。 |
| 无符号字符型                                                       | **Track3EncryptedDataLength** -如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)为**MsrDataEncryption\_None**，将始终为零（0）。 |
| 无符号字符型                                                       | **Track4EncryptedDataLength** -如果[MsrDataEncryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)为**MsrDataEncryption\_None**，将始终为零（0）。 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道1数据的**Track1EncryptedDataLength**字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道2数据的**Track2EncryptedDataLength**字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道3数据的**Track3EncryptedDataLength**字节                                                                         |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道4数据的**Track4EncryptedDataLength**字节                                                                         |
| 无符号字符型                                                       | **Track1MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track2MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track3MaskedDataLength**                                                                                                            |
| 无符号字符型                                                       | **Track4MaskedDataLength**                                                                                                            |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 屏蔽轨迹1数据的**Track1MaskedDataLength**字节数                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2MaskedDataLength** bytes of 遮掩 track 2 数据                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3MaskedDataLength** bytes of 遮掩 track 3 数据                                                                               |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4MaskedDataLength** bytes of 遮掩 track 4 数据                                                                               |
| 无符号字符型                                                       | 如果**MagneticStripeReaderIsDecodeDataEnabled**为 false，则**Track1DiscretionaryDataLength** –将始终为零（0）。                |
| 无符号字符型                                                       | 如果**MagneticStripeReaderIsDecodeDataEnabled**为 false，则**Track2DiscretionaryDataLength**–将始终为零（0）。                 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 任意磁道1数据的**Track1DiscretionaryDataLength**字节数                                                                 |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 随机跟踪2数据的**Track2DiscretionaryDataLength**字节数                                                                 |
| 无符号字符型                                                       | **CardAuthenicationDataLength** -加密数据的长度（以字节为单位），包括填充                                            |
| 无符号字符型                                                       | **CardAuthenticationDataAbsoluteLength** -未加密数据的长度（以字节为单位）（可能需要在解密过程中去除填充）  |
| 无符号 char\[MSR\_其他\_安全\_信息\_数据\_大小\] | 卡身份验证数据的**CardAuthenticationDataAbsoluteLength**字节数                                                            |
| 无符号字符型                                                       | **AdditionalSecurityInformationLength**                                                                                               |
| 无符号 char\[MSR\_额外\_安全\_信息\_大小\]       | 额外安全信息的**AdditionalSecurityInformationLength**字节数                                                      |

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
