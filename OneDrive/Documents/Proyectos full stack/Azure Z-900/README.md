# Azure Z-900 Essentials: Guía Completa

## Índice
1. [Introducción a Azure y Costos](#introducción-a-azure-y-costos)
2. [Primeros Pasos en Azure](#primeros-pasos-en-azure)
3. [Herramientas de Infraestructura como Código](#herramientas-de-infraestructura-como-código)
4. [Configuración de Entornos de Desarrollo](#configuración-de-entornos-de-desarrollo)
5. [Herramientas de Administración de Azure](#herramientas-de-administración-de-azure)
6. [Implementación de Aplicaciones Serverless](#implementación-de-aplicaciones-serverless)
7. [Configuración de DNS en Azure](#configuración-de-dns-en-azure)

## Introducción a Azure y Costos

### Aspectos Fundamentales de Cotización
Al trabajar con Azure, las Máquinas Virtuales (VMs) son típicamente el primer recurso que se debe cotizar para cualquier proyecto. Estas forman la base de muchos servicios en la nube.

### Configuración para Equipos de Desarrollo
Para un equipo pequeño de desarrollo (hasta 5 desarrolladores) que necesite desplegar hasta 3 aplicaciones web, se puede estimar un costo mensual entre $155 y $230 dólares (aproximadamente $1,860 - $2,760 dólares anuales).

Esta estimación incluye:
- Servidores virtuales para desarrollo
- Servicios de almacenamiento
- Servicios de red básicos
- Servicios de aplicaciones web

> **Consejo**: Utiliza la [Calculadora de Precios de Azure](https://azure.microsoft.com/es-es/pricing/calculator/) para obtener estimaciones más precisas según tus necesidades específicas.

## Primeros Pasos en Azure

1. **Crear una cuenta de Azure**:
   - Visita [portal.azure.com](https://portal.azure.com)
   - Regístrate con una cuenta de Microsoft
   - Proporciona información de facturación

2. **Registrar una tarjeta de crédito**:
   - Requerido para activar la cuenta
   - Se ofrece un crédito gratuito para nuevos usuarios ($200 durante los primeros 30 días)
   - Acceso a servicios gratuitos durante 12 meses

> **Nota**: Aunque se requiere una tarjeta de crédito, Microsoft no realizará cargos sin tu autorización después de que se agote el crédito gratuito.

## Herramientas de Infraestructura como Código

El despliegue de recursos en Azure puede realizarse mediante diferentes herramientas de Infraestructura como Código (IaC):

### Bicep
Bicep es un lenguaje declarativo desarrollado por Microsoft específicamente para Azure Resource Manager (ARM). Ofrece una sintaxis más sencilla y legible que las plantillas JSON tradicionales.

**Ventajas de Bicep**:
- Sintaxis más concisa y fácil de leer que JSON
- Soporte nativo en Azure
- Excelente integración con Visual Studio Code
- Conversión bidireccional entre Bicep y plantillas ARM

### Plantillas ARM
Son documentos JSON que definen la infraestructura y configuración de los recursos de Azure.

### Proveedor AzAPI de Terraform
Terraform es una herramienta de IaC multiplataforma que permite definir recursos en varios proveedores de nube, incluyendo Azure.

## Configuración de Entornos de Desarrollo

### Visual Studio Code con Extensión Bicep

1. **Instalación de Visual Studio Code**:
   - Descargar desde [code.visualstudio.com](https://code.visualstudio.com)

2. **Instalación de la Extensión Bicep**:
   - Abrir VS Code
   - Ir a la pestaña de Extensiones (Ctrl+Shift+X)
   - Buscar "Bicep"
   - Seleccionar "Instalar"

3. **Verificación de la Instalación**:
   - Abrir cualquier archivo con extensión `.bicep`
   - El modo de lenguaje en la esquina inferior derecha debería cambiar a "Bicep"

4. **Configuración de la Extensión**:
   - Opciones personalizables como decompileOnPaste, enableOutputTimestamps, etc.

### Azure CLI

La CLI de Azure es una herramienta de línea de comandos que permite administrar recursos de Azure desde prácticamente cualquier plataforma.

**Instalación**:
- **Windows**: Descargar el instalador MSI
- **Linux**: Utilizar comandos específicos según la distribución
- **macOS**: Utilizar Homebrew o script de instalación

**Comandos Básicos**:
```bash
# Verificar versión
az --version

# Verificar instalación de Bicep
az bicep version

# Actualizar a la última versión
az bicep upgrade
```

### Azure PowerShell

Alternativa a Azure CLI para usuarios de Windows, requiere:
- Versión 5.6.0 o posterior
- Instalación manual de la CLI de Bicep

## Herramientas de Administración de Azure

### Azure Cloud Shell
Interfaz de línea de comandos basada en navegador que proporciona acceso a herramientas de Azure sin necesidad de instalación local.

### Monitoreo de Azure Service Health
Permite supervisar el estado de los servicios de Azure en diferentes regiones:
- Acceso mediante: [status.azure.com](https://status.azure.com/es-es/status)
- Ofrece información sobre:
  - Interrupciones de servicio
  - Eventos de mantenimiento planificado
  - Avisos de estado

### Portales de Administración

1. **Portal de Microsoft Entra ID** (anteriormente Azure AD):
   - [entra.microsoft.com](https://entra.microsoft.com/#home)
   - Configuración de directivas de seguridad
   - Administración de identidades

2. **Azure AI Portal**:
   - Para gestión de servicios de IA en Azure
   - Acceso a Azure AI Foundry

3. **Azure Machine Learning Studio**:
   - Desarrollo de modelos de IA para machine learning
   - Entorno de trabajo colaborativo

4. **Azure Data Factory**:
   - Servicio de integración de datos en la nube
   - Automatización del movimiento y transformación de datos

## Implementación de Aplicaciones Serverless

Las aplicaciones serverless permiten ejecutar código sin preocuparse por la infraestructura subyacente. Azure Functions es el servicio principal para este tipo de implementaciones.

### Pasos para Implementar una Aplicación Serverless:

1. **Crear un Grupo de Recursos**:
   ```bash
   az group create --name MyServerlessGroup --location eastus
   ```

2. **Crear una Cuenta de Almacenamiento** (necesaria para las funciones):
   ```bash
   az storage account create --name mystorageaccount --resource-group MyServerlessGroup --location eastus --sku Standard_LRS
   ```

3. **Crear una Function App**:
   ```bash
   az functionapp create --name MyFunctionApp --resource-group MyServerlessGroup --storage-account mystorageaccount --consumption-plan-location eastus --runtime node
   ```

4. **Desplegar el Código de la Función**:
   - Puede realizarse mediante VS Code, Azure CLI o Azure DevOps

> **Ventajas**: Con las aplicaciones serverless, el usuario final no necesita preocuparse por ningún aspecto relacionado con los servidores, como el escalado, la disponibilidad o el mantenimiento.

## Configuración de DNS en Azure

### Registros DNS Comunes en Azure

Para redirigir el tráfico de un dominio a una dirección específica en Azure, es necesario crear un **Registro A**. Este registro mapea un nombre de dominio a una dirección IPv4.

**Ejemplo de Creación de un Registro A**:
```bash
az network dns record-set a add-record -g MyResourceGroup -z example.com -n www -a 192.0.2.42
```

### Pasos para Gestionar Zonas DNS en Azure:

1. **Crear una Zona DNS**:
   ```bash
   az network dns zone create -g MyResourceGroup -n example.com
   ```

2. **Añadir un Registro A**:
   ```bash
   az network dns record-set a add-record -g MyResourceGroup -z example.com -n www -a 192.0.2.42
   ```

3. **Verificar los Registros DNS**:
   ```bash
   az network dns record-set a show -g MyResourceGroup -z example.com -n www
   ```

4. **Actualizar los Servidores de Nombres** en el registrador de dominios para que apunten a los servidores de nombres de Azure.

> **Importante**: Después de crear o modificar registros DNS, los cambios pueden tardar hasta 48 horas en propagarse completamente por Internet, aunque generalmente ocurre en cuestión de minutos u horas.

---

Este documento es un resumen de las notas del curso Azure Z-900 Essentials. Para información más detallada y actualizada, consulte la [documentación oficial de Microsoft Azure](https://learn.microsoft.com/es-es/azure/).
