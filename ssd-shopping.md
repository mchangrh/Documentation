# Physical Interfaces

## SATA:
| Revision | Speed   | Throughput |
|----------|---------|------------|
| SATA I   | 1.5Gb/s | 150MB/s    |
| SATA II  | 3.0Gb/s | 300MB/s    |
| SATA III | 6.0Gb/s | 600MB/s    |

## PCI-E:
| Generation | Width | Speed    |
|------------|-------|----------|
| PCIe 3.0   | 2     | 1970MB/s |
|            | 4     | 3940MB/s |
| PCIe 4.0   | 2     | 3940MB/s | 
|            | 4     | 7880MB/s |

## USB:
 - USB-C is only a connector and can carry signals from USB2 (400MB/s) to USB3.2 (20Gbps)
 - USB-A is the wider and more recognizable non-reversable interface  

# Device Interfaces/ Protocols
 - NVMe (NVM Express) - Default for M.2 PCI Express SSDs - able to handle higher IO loads, not compatible with SATA
 - SATA - Limited to the speeds of the SATA interface
 - UASP (USB Attached SCSI Protocol) - Speeds USB-Attached storage devices (only on USB3.0+)

# Form Factors:

## mSata
Mini-SATA - wider than M.2, common in older laptops and netbooks

## M.2 / NNFF (Next Generation Form Factor)
measured in milimeters - 2280 is 22mm wide and 80mm wide

### M.2 Keying
- B+M (Two notches on both ends) - SATA SSD - Max 550MB/s
 - M (Single notch) - NVMe SSD - Max 3940MB/s (PCIe 3) / 7880MB/s (PCIe 4)

## Disk/ Drive
5.25":
 - CD/ DVD/ BluRay Drive Bays

3.5":
 - mostly large capacity desktop hard drives

2.5":
 - 7mm: slightly shorter 2.5" SSD
 - 9mm: slightly taller 2.5" HDD

# SLC/ MLC/ TLC/ QLC
how many layers of NAND storage are on a single area
 - more layers means worse sustained performance
 - more layers means worse lifespan
 - more layers means significantly cheaper

3D NAND usually means TLC

# Shopping
 - If an SSD advertises speeds of up to 550MB/s - it's a SATA SSD
 - tl;dr - NVME = PCIe = M.2 M KEY


# tl;dr
- M.2
  - NVME = PCIe = M.2 M Key
  - B+M / M are not compatible
  - M (3970MB/s) > B+M (550MB/s)
- if an SSD runs at 550M/s it is SATA or B+M
- NVME is marginally more expensive ($94.99 vs $89.99)
