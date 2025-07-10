
# El-Capul-n-para-Windows-11
Esta guía proporciona comandos eficientes para instalar software clave en tu sistema Windows 11 utilizando Winget y Chocolatey. Está diseñada para automatizar la configuración inicial de tu entorno de desarrollo y uso general, así como para incluir herramientas adicionales y personalizaciones.This document outlines commands for installing software on Windows 11 using Winget and Chocolatey, and provides scripts for system preparation, software installation, and system customization.



### Tabla de Contenidos

1.  [Preparación del Sistema](#preparación-del-sistema)
    * [Winget](#winget)
    * [Chocolatey](#chocolatey)
2.  [Instalación de Software Esencial](#instalación-de-software-esencial)
    * [Brave Browser](#brave-browser)
    * [7-Zip](#7-zip)
    * [WinRAR](#winrar)
    * [CPU-Z](#cpu-z)
    * [TranslucentTB](#translucenttb)
    * [Git](#git)
    * [Python 3.10](#python-310)
    * [Visual Studio Code](#visual-studio-code)
3.  [Personalización y Utilidades del Sistema](#personalización-y-utilidades-del-sistema)
    * [Configuración de Terminal de Windows: PowerShell 5 -> PowerShell 7](#configuración-de-terminal-de-windows-powershell-5---powershell-7)
    * [Aceleración del Ratón](#aceleración-del-ratón)
    * [Centrar Elementos de la Barra de Tareas](#centrar-elementos-de-la-barra-de-tareas)
    * [Mostrar Extensiones de Archivo](#mostrar-extensiones-de-archivo)
    * [Scripts de Activación de Microsoft (MAS)](#scripts-de-activación-de-microsoft-mas)
4.  [Herramientas de Desarrollo](#herramientas-de-desarrollo)
    * [Windows Terminal](#windows-terminal)
    * [PowerShell 4.5](#powershell-45)
    * [Redistribuibles de Visual C++ para Visual Studio 2015](#redistribuibles-de-visual-c-para-visual-studio-2015)
5.  [Guía de Instalación de Python y Herramientas](#guía-de-instalación-de-python-y-herramientas)
    * [Python](#python)
    * [Pip (Gestor de Paquetes Python)](#pip-gestor-de-paquetes-python)
    * [JupyterLab](#jupyterlab)
    * [Jupyter Notebook](#jupyter-notebook)
    * [Voilà](#voilà)
    * [Miniconda](#miniconda)
    * [Mamba](#mamba)
    * [Pipenv](#pipenv)
    * [Homebrew (Solo para macOS y Linux)](#homebrew-solo-para-macos-y-linux)
6.  [Configuración Avanzada de Terminal y Shell](#configuración-avanzada-de-terminal-y-shell)
    * [Emuladores de Terminal](#emuladores-de-terminal)
    * [Multiplexores de Terminal](#multiplexores-de-terminal)
    * [Mejoras de Shell](#mejoras-de-shell)
7.  [Herramientas de Desarrollo Especializadas](#herramientas-de-desarrollo-especializadas)
    * [Desarrollo Android](#desarrollo-android)
    * [Análisis de Datos con Python](#análisis-de-datos-con-python)
    * [Virtualenv](#virtualenv)
8.  [Herramientas para USB Booteable](#herramientas-para-usb-booteable)
    * [Rufus v4.4](#rufus-v44)
    * [Multibootusb](#multibootusb)
9.  [Herramientas de Red Inalámbrica](#herramientas-de-red-inalámbrica)
    * [PENetwork](#penetwork)
10. [Software de Particiones](#software-de-particiones)
    * [EasyBCD](#easybcd)
    * [DiskGenius](#diskgenius)
    * [Wizard Partition](#wizard-partition)
11. [Visores de Documentos](#visores-de-documentos)
    * [Sumatra PDF](#sumatra-pdf)
12. [Notas de Configuración Avanzada](#notas-de-configuración-avanzada)



## 1. Preparación del Sistema

Antes de instalar las aplicaciones, es crucial asegurarse de que tus gestores de paquetes estén listos. Ejecuta tu terminal 


 administrador.

### Winget

**Descripción:** Winget es el gestor de paquetes oficial de Windows. Te permite instalar, actualizar y gestionar aplicaciones directamente desde la línea de comandos, agilizando enormemente la configuración del sistema.

**Comando de Instalación/Actualización:**

``` cmd
powershell.exe -NoProfile -ExecutionPolicy Bypass -Command "$v = winget -v; if ([version]($v.TrimStart('v')) -lt [version]'1.7.0') { Write-Output 'Old winget version detected, upgrading...'; Set-Location $env:USERPROFILE; Invoke-WebRequest -Uri '[https://aka.ms/getwinget](https://aka.ms/getwinget)' -OutFile 'winget.msixbundle'; Add-AppPackage -ForceApplicationShutdown .\winget.msixbundle; Remove-Item .\winget.msixbundle } else { Write-Output 'Winget is already up to date, skipping upgrade.' }"

Notas:
 * Ejecuta este comando en una ventana de PowerShell o CMD elevada (como administrador).
 * Verifica tu versión actual de Winget y la actualiza si es anterior a la 1.7.0.
Chocolatey
Descripción: Chocolatey es un robusto gestor de paquetes para Windows que funciona sin problemas con herramientas de línea de comandos como PowerShell. Proporciona acceso a un vasto repositorio de aplicaciones y herramientas, lo que facilita y hace repetibles las instalaciones.
Comando de Instalación:
powershell.exe -NoProfile -ExecutionPolicy Bypass -Command "Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('[https://community.chocolatey.org/install.ps1](https://community.chocolatey.org/install.ps1)'))"

Notas:
 * Ejecuta este comando en una ventana de PowerShell elevada (como administrador).
 * Después de la instalación, cierra y vuelve a abrir tu terminal para asegurarte de que Chocolatey se haya añadido al PATH de tu sistema.
2. Instalación de Software Esencial
Esta sección detalla la instalación de varias aplicaciones de software esenciales utilizando los gestores de paquetes configurados previamente.
Brave Browser
Descripción: Brave es un navegador web rápido, privado y seguro, con un bloqueador de anuncios integrado y protección contra el rastreo, mejorando tu experiencia en línea.
Comando para CMD:
winget install Brave.Brave --accept-source-agreements --accept-package-agreements --force

7-Zip
Descripción: 7-Zip es un archivador de archivos gratuito y de código abierto para Windows con una alta relación de compresión, compatible con una amplia gama de formatos de archivo.
Comando para CMD:
winget install 7zip.7zip --accept-source-agreements --accept-package-agreements --force

WinRAR
Descripción: WinRAR es una potente utilidad de compresión de archivos que te permite crear, gestionar y extraer archivos en formato RAR y ZIP, entre otros.
Comando para CMD:
winget install RARLab.WinRAR --accept-source-agreements --accept-package-agreements --force

CPU-Z
Descripción: CPU-Z es una utilidad gratuita que proporciona información detallada sobre los principales dispositivos de tu sistema, incluyendo el nombre del procesador, la velocidad del núcleo y las especificaciones de la memoria.
Comando para CMD:
winget install CPUID.CPU-Z --accept-source-agreements --accept-package-agreements --force

TranslucentTB
Descripción: TranslucentTB es una utilidad ligera que hace que la barra de tareas de Windows sea translúcida o completamente transparente, ofreciendo una estética de escritorio más limpia.
Comando para CMD:
winget install CharlesMilette.TranslucentTB --accept-source-agreements --accept-package-agreements --force

Git
Descripción: Git es un sistema de control de versiones distribuido esencial para el desarrollo de software. Te permite rastrear cambios en el código, colaborar con otros y gestionar el historial del proyecto.
Comando para CMD:
winget install Git.Git --accept-source-agreements --accept-package-agreements --force

Python 3.10
Descripción: Python es un lenguaje de programación versátil y de alto nivel ampliamente utilizado para el desarrollo web, análisis de datos, inteligencia artificial y más. Este comando instala la versión 3.10.
Comando para CMD:
winget install Python.Python.3.10 --accept-source-agreements --accept-package-agreements --force

Visual Studio Code
Descripción: Visual Studio Code (VS Code) es un editor de código fuente gratuito, potente y ligero desarrollado por Microsoft. Soporta varios lenguajes de programación y ofrece una amplia personalización a través de extensiones.
Comando para CMD:
winget install Microsoft.VisualStudioCode --accept-source-agreements --accept-package-agreements --force

3. Personalización y Utilidades del Sistema
Esta sección cubre varios ajustes y utilidades ese
