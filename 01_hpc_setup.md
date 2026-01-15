# HPC Setup Notes

**Date:** 2026-03-27  
**HPC System:** QIMRBerghofer Avalon (`hpcbs01.adqimr.ad.lan`)  
**Username:** yanC

---

## Connection

- SSH client: MobaXterm v26.1
- X11 forwarding: enabled (required for IGV)
- Login node: `hpcbs01`

> ⚠️ The login node is for file management and job submission only.  
> All computational work must be submitted via `qsub`.

---

## Key Commands

```bash
# Navigate to lab data directory
LabData          # returns user ID (792589)

# Project data location
cd /working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/example_data/

# Load IGV
module load igv/2.18.2
igv.sh
```

---

## Project Data

- **Location:** `/working/genomeinfo/share/analysis/Yan_Chen_Masters_Project/`
- **Example data:** `example_data/` (RNA-seq BAM file — being copied by Dean)

---

## Software Modules

| Tool | Version | Command |
|------|---------|---------|
| IGV  | 2.18.2  | `module load igv/2.18.2` |

---

## Local Setup (Laptop)

| Tool | Purpose |
|------|---------|
| MobaXterm | SSH client + X11 forwarding |
| IGV (local) | View downloaded BAM/screenshots |
| FileZilla | Transfer files between laptop and HPC |
| VSCode + Git Bash | Scripts and code |

---

## Wiki References

- [PBS Job Submission](https://genomeinfo.qimrberghofer.edu.au/wiki/HPC/PBS)
- [Avalon HPC Guide](https://genomeinfo.qimrberghofer.edu.au/wiki/HPC/Avalon)
- [User Induction](https://genomeinfo.qimrberghofer.edu.au/wiki/HPC/UserInduction)
- [IGV on HPC](https://genomeinfo.qimrberghofer.edu.au/wiki/IGV)
