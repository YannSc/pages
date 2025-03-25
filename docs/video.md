# Video

## AVCC vs AnnexB

### AVCC (Advanced Video Coding Configuration)

    Container Compatibility: Typically used in MP4, MOV, and other modern container formats.
    NALU (Network Abstraction Layer Unit) Separation: Uses a length-prefixed format. Each NALU is preceded by a 4-byte length field that indicates the size of the NALU.
    Usage: Commonly used for storage and streaming where the container format can handle the length-prefix.
    Advantages: More efficient for parsing as the length of each NALU is known in advance, allowing for easier extraction and processing.
    References:
        ISO/IEC 14496-15:2004 (MPEG-4 Part 15) - Describes the storage format for H.264/AVC in MP4 files.
        ITU-T H.264 (also known as MPEG-4 AVC) - Defines the codec.

### Annex B

    Container Compatibility: Often used in TS (Transport Stream) and similar container formats.
    NALU Separation: Uses start code prefixes (0x000001 or 0x00000001) to indicate the beginning of each NALU.
    Usage: Commonly used for broadcasting and real-time streaming where the start code can help in quick synchronization and error recovery.
    Advantages: Start codes are useful for real-time streaming and error recovery as they provide clear demarcation of NALUs which can be detected even in the presence of transmission errors.
    References:
        ITU-T H.264 (also known as MPEG-4 AVC) - Defines the codec and includes Annex B as one of the possible formats for NALU separation.
        ISO/IEC 13818-1 (MPEG-2 Part 1) - Defines the transport stream format.

MP4 format supports AVCC, avi format supports AnnexB

## ACC vs G711 format

G711 (u or a law) are stored as raw buffers which can be sent for decoding without preprocessing.

AAC buffers requires the creation of ADTS frames to specify context and decoding informations. 


    The ADTS header is a fixed-length header that precedes each AAC frame. It contains metadata about the AAC frame, such as the frame length, sampling rate, and channel configuration.
    The ADTS header is 7 or 9 bytes long, depending on whether the CRC (Cyclic Redundancy Check) is used.

ADTS Header Structure:

    The ADTS header is composed of several fields, each with a specific bit length. Here’s the structure of the ADTS header:
    Code

| Bits | Field                      | Description |
|------|----------------------------|-------------|
| 12   | Syncword                   | 0xFFF, all bits must be 1 |
| 1    | ID                         | MPEG Version: 0 for MPEG-4, 1 for MPEG-2 |
| 2    | Layer                      | Always 00 |
| 1    | Protection_absent          | 1 if no CRC, 0 if CRC present |
| 2    | Profile                    | Profile of AAC: 00 Main, 01 LC (Low Complexity), 10 SSR (Scalable Sample Rate) |
| 4    | Sampling_frequency_index   | Sampling rate index (4 bits) |
| 1    | Private_bit                | Usually 0 |
| 3    | Channel_configuration      | Channel configuration (3 bits) |
| 1    | Original/copy              | 0 for original, 1 for copy |
| 1    | Home                       | Always 0 |
| 1    | Copyright_identification_bit| 0 or 1 |
| 1    | Copyright_identification_start | 0 or 1 |
| 13   | Frame_length               | Length of the frame including header |
| 11   | Buffer_fullness            | 0x7FF if VBR, otherwise buffer fullness |
| 2    | Number_of_raw_data_blocks_in_frame | Usually 0 |
