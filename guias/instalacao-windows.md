# Como instalar o TivaWare no Windows

Os arquivos necessários são:
- `TivaWare_C_Serie - SW-TM4C-2.2.0.295.exe`
- `stellaris_icdi_drivers.zip`
- `MDK539.exe`
- `MDK_Stellaris_ICDI_AddOn.exe`
## MDK - Microcontroller Development Kit
1. Execute o `MDK539.exe
`next -> agree + next`

2. Configure os locais dos arquivos
- Core: onde a aplicação vai ficar
- Pack: onde os packs baixados pelo pack manager vão ficar

Configurei os meus pro seguinte:

`Core: D:\src\Keil_v5`
`Pack: D:\src\Keil_v5\packs`

E aperta **next**.

3. Em **Costumer Information**, preencha os dados com o que você quiser, não faz diferença.

Ao longo da instalação, ele vai unzipar um monte de coisa e te pedir permissão pra instalar uns drivers. Clique em **Instalar**.

## Instalação do pack pra Tiva

Quando você finalizar a instalação do MDK, ele vai abrir no Pack Installer. Caso não abra, basta ir até a pasta UV4 e procurar por `PackInstaller.exe`

No caminho que configurei, ficou:

`D:\src\Keil_v5\UV4\PackInstaller.exe`

1. No painel esquerdo, procure por Texas Instruments
2. Expanda e encontre `Tiva C Series` (tá bem no final)
3. Clique em `Tiva C Series`
4. Na lateral direita, na aba `Packs` instale o primeiro, que diz

```
- Device Specific
 ┗ Keil::TM4C_DFP | [ Install ] | Texas Instruments Tiva C Series Device Support and Examples
```

5. Clique em `Install`!