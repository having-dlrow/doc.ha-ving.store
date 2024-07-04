# File System

## Archiving and Compressing File

<table><thead><tr><th width="146">compress</th><th>command</th></tr></thead><tbody><tr><td>gzip</td><td><pre><code>sudo tar -cvzf home.tgz /home
</code></pre></td></tr><tr><td>bz2</td><td><pre><code>sudo tar -cjvf home.tbz2 /home
</code></pre></td></tr><tr><td>xz</td><td><pre><code>sudo tar -cJvf home.xz /home
</code></pre></td></tr></tbody></table>

## Logical Volume Manager

<details>

<summary>물리적 저장 공간을 논리적 볼륨으로 관리하고 조정합니다.</summary>

#### 생성

```
lvcreate -n lv01 -L 10G vg01
```

#### 크기 확장

```
lvextend -L +10G /dev/vg01/lv01
```

#### 크기 축소

```
lvreduce -L -5G /dev/vg01/lv01
```

</details>

## Assembling partitions RAID

<details>

<summary>여러 디스크를 하나로 묶어 RAID 배열을 생성하고 관리합니다.</summary>

#### RAID 생성&#x20;

3개의 디스크(`/dev/sdb`, `/dev/sdc`, `/dev/sdd`)를 사용하여 RAID 5 배열을 생성

```
mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
```

#### RAID 배열 상태 확인

```
mdadm --detail /dev/md0
```

#### RAID 배열에 디스크 추가

```
mdadm --add /dev/md0 /dev/sde
```

#### RAID 배열에서 디스크 제거

```
mdadm /dev/md0 --fail /dev/sdd
mdadm /dev/md0 --remove /dev/sdd
```

</details>

## Format File System

<details>

<summary>파일 시스템을 포맷합니다 (예: ext4, xfs 등)</summary>

#### ext4

```
mkfs.ext4 /dev/sdb1
```

#### xfs

```
mkfs.xfs /dev/sdb2
```

</details>

## Mount File System at Boot Time

<details>

<summary>부팅 시 파일 시스템을 자동으로 마운트하도록 설정합니다.</summary>

#### /etc/fstab

```
/dev/sdb1 /data ext4 defaults 0 2

# /dev/sdb1: 마운트할 디바이스 또는 파티션
# /data: 마운트 포인트(파일 시스템을 마운트할 디렉토리)
# ext4: 파일 시스템 유형
# defaults: 마운트 옵션 (기본 옵션 사용)
# 0: 덤프 옵션 (0은 덤프되지 않음을 의미)
# 2: 파일 시스템 검사 순서 (루트 파일 시스템이 아닌 경우 2)
```

</details>

## Mount Network File System

<details>

<summary>네트워크 파일 시스템 (NFS)을 로컬 시스템에 마운트합니다.</summary>

Mount

```
mount -t nfs 192.168.1.100:/share /mnt/nfs
```

</details>

## Partitioning Storage Device

<details>

<summary>스토리지 디바이스를 파티셔닝합니다.</summary>

`fdisk`와 `parted`는 스토리지 디바이스를 파티셔닝하는 데 사용되는 도구입니다.

#### fdisk

```
fdisk /dev/sdb

# 새파티션 생성 : n
# 저장 : w
```

#### parted

```
parted /dev/sdb

# GPT 파티션 테이블을 생성합니다
mklabel gpt 

# 1MiB에서 100MiB 사이에 primary ext4 파티션을 생성합니다
mkpart primary ext4 1MiB 100MiB 
```

</details>

## Swap Partition

<details>

<summary>SWAP 영역을 생성하고 활성화/비활성화합니다.</summary>

#### SWAP 공간 생성(초기화)

```bash
mkswap /dev/sdb1
```

#### SWAP 활성

```bash
swapon /dev/sdb1
```

#### SWAP 비활성화

```bash
swapoff /dev/sdb1
```

</details>

