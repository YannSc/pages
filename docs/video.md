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

## 