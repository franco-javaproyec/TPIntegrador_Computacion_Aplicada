# TPIntegrador_Computacion_Aplicada
Tp Integrador Grupo 8
Universidad de Palermo
Año 2025  
Integrantes: Matias Ezequiel Sucharkiewicz, Ricardo Belevan, Franco Casorla y Tamara Lis Ferreyra.

## Contenido del repositorio

Este repositorio contiene los entregables solicitados en el Punto 6 del TP Integrador:

- [root.tar.gz](./root.tar.gz) → contiene el directorio `/root`
- [etc.tar.gz](./etc.tar.gz) → contiene el directorio `/etc`
- [opt.tar.gz](./opt.tar.gz) → contiene el directorio `/opt`
- [www_dir.tar.gz](./www_dir.tar.gz) → contiene el directorio `/www_dir`
- [backup_dir.tar.gz](./backup_dir.tar.gz) → contiene el directorio `/backup_dir`

Archivos del directorio `/var` (comprimido y spliteado según la consigna):

- [var_part_aa](./var_part_aa)
- [var_part_ab](./var_part_ab)
- [var_part_ac](./var_part_ac)
- [var_part_ad](./var_part_ad)


## 🖥️ Diagrama Topológico de la Infraestructura Armada

```
                       ┌────────────────────────────────┐
                       │     Máquina Física (Windows)   │
                       │--------------------------------│
                       │  - Navegador Web               │
                       │  - PowerShell / SSH            │
                       │  - Clave Privada (SSH)         │
                       │  - GitHub                      │
                       └───────────────┬────────────────┘
                                       │
                                       │  Red Física Hogar / LAN
                                       │  (192.168.0.0/24)
                                       │
                 IP: 192.168.0.38      │
        ┌──────────────────────────────┼──────────────────────────────┐
        │                              │                              │
        ▼                              ▼                              ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                Oracle VirtualBox – HOST (Windows ejecutando VM)          │
└──────────────────────────────────────────────────────────────────────────┘
                                       │
                                       │ Adaptador Puente (Bridge)
                                       │
                 IP: 192.168.0.38      │
        ┌──────────────────────────────┘
        ▼
┌──────────────────────────────────────────────────────────────────────────┐
│       Máquina Virtual Debian 11 – TPServer (Servidor del TP)             │
│──────────────────────────────────────────────────────────────────────────│
│  Hostname: TPServer                                                      │
│                                                                          │
│  Servicios Instalados:                                                   │
│   • SSH (root por clave pública)                                         │
│   • Apache + PHP (index.php + logo.png)                                  │
│   • MariaDB (db.sql importado)                                           │                                                                          
│  Configuración de Red:                                                   │
│   • Interfaz: enp0s3                                                     │
│   • IP estática: 192.168.0.38                                            │
│   • Gateway: 192.168.0.1                                                 │
│   • Accesible desde Windows (SSH y navegador)                            │
│                                                                          │
│  Disco Principal (VM):                                                   │
│   • Sistema operativo Debian 11                                          │
│   • Servicios Apache/SSH/MariaDB                                         │
│   • Archivos del sistema (root, etc, var, etc.)                          │
│                                                                          │
│  Disco Secundario (10 GB) creado para el TP:                             │
│   /dev/sdc                                                               │
│     ├─ /dev/sdc1 (3 GB) → montado en /www_dir                            │
│     │       • index.php                                                  │
│     │       • db.sql                                                     │
│     │       • contenido web                                              │
│     │                                                                    │
│     └─ /dev/sdc2 (6 GB) → montado en /backup_dir                         │
│             • backups automáticos                                        │
│                                                                          │
│  Automatizaciones:                                                       │
│   • /opt/particion generado al inicio (@reboot)                          │
│   • backup_full.sh en /opt/scripts                                       │
│   • CRON:                                                                |
│       - 00:00 → backup /var/logs                                         │
│       - L/M/V 23:00 → backup /www_dir                                    │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```



