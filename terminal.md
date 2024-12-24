# Terminal

### Instalacion
* **Instalar Posh:** winget install JanDeDobbeleer.OhMyPosh s winget

* **Actualizar:** winget upgrade JanDeDobbeleer.OhMyPosh s winget

* **Verificar Posh:** oh-my-posh

* **Cargar tema defaut:** oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json"

* **Copiar ruta que devuelve, pegas y dar enter** 

* **Ver temas:** 

* **Selecionar tema y copiar nombre**

* **Abrir Archivo Config Perful:** notepad $PROFILE (Crear: New-Item -Path $PROFILE -Type File -Force)

* **Instalar icons:** Install-Module -Name Terminal-Icons -Repository PSGallery

---

### Configuracion
* **Abrir configuracion de perfil**

* **Poner**
    * **Tema:** (@(& 'C:/Users/pipea/AppData/Local/Programs/oh-my-posh/bin/oh-my-posh.exe' init pwsh --config='C:\Users\pipea\AppData\Local\Programs\oh-my-posh\themes\nombreTema.omp.json' --print) -join "`n") | Invoke-Expression

    * **Tema Git:** eval "$(oh-my-posh init bash --config ~/AppData/Local/Programs/oh-my-posh/themes/nombreTema.omp.json)"

    * **Iconos:** Import-Module Terminal-Icons

    * **Autocomplete History:** Set-PSReadLineOption -PredictionViewStyle ListView

* **Extra**
    * **Sacar ruta de los temas y copiar:** $env:POSH_THEMES_PATH

    * **Abrir en explorador:** explorer (ruta)

