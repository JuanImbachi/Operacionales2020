# POWERSHELL Clase 5

## ASPECTOS BÁSICOS DE WMI Y CIM

## EJERCICIOS
1. ¿Cuál clase puede emplearse para consultar la dirección IP de un adaptador
   de red? ¿Posee dicha clase algún método para liberar un préstamo de
   dirección (lease) DHCP?

   ```powershell
    Get-WmiObject Win32_NetworkAdapterConfiguration | select -Property IP
    ```
    ```powershell
    Para liberar un préstamo de dirección DHCP se tiene el método ReleaseDHCPLease()
    ```

2. Despliegue una lista de parches empleando WMI (Microsoft se refiere a los
   parches con el nombre **quick-fix engineering**). Es diferente el listado al
   que produce el cmdlet ``Get-Hotfix``?

    ```powershell
    Get-WmiObject Win32_QuickFixEngineering
    Produce el mismo resultado que el cmdlet ``Get-Hotfix``
    ``` 

3. Empleando WMI, muestre una lista de servicios, que incluya su status actual,
   su modalidad de inicio, y las cuentas que emplean para hacer login.

    ```powershell
    Get-WmiObject Win32_Service | select -Property Name, Status, StartMode, StartName 
    ``` 

4. Empleando cmdlets de CIM, liste todas las clases del namespace
   ``SecurityCenter2``, que tengan **product** como parte del nombre.

    ```powershell
    Get-CimClass -Namespace root\SecurityCenter2 | where cimclassname -Like '*product*'
    ``` 

5. Empleando cmdlets de CIM, y los resultados del ejercicio anterior, muestre
   los nombres de las aplicaciones antispyware instaladas en el sistema.
   También puede consultar si hay productos antivirus instalados en el sistema.

    ```powershell
    Get-CimInstance -Namespace root\SecurityCenter2 -ClassName AntiSpywareProduct| select -Property displayName
    Get-CimInstance -Namespace root\SecurityCenter2 -ClassName AntiVirusProduct | select -Property displayName
    ```    