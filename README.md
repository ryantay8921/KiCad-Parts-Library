# RT_Lib: ready-to-place JLCPCB parts for KiCad

1475 symbols, one physical part each: value, size, footprint, LCSC, MPN, manufacturer,
datasheet and JLC class already filled in. Full set list: RT_Lib_Catalog.csv.

```
RT_Lib/
  symbols/
    Resistors/     RT_R_0402  RT_R_0603  RT_R_0805
    Capacitors/    RT_C_0402  RT_C_0603  RT_C_0805  RT_C_1206
    Inductors/     RT_L_Chip  RT_FerriteBead
    Diodes/        RT_D_Switching  RT_D_Rectifier  RT_D_Schottky  RT_D_Zener  RT_D_TVS
    LEDs/          RT_LED
    Transistors/   RT_Q_MOSFET  RT_Q_BJT
  ics/             RT_ICs (symbols, .pretty footprints, 3D models from LCSC)
  sym-lib-table_RT_Lib.txt   lines to paste into KiCad's global symbol table
  fp-lib-table_RT_Lib.txt    line to paste into KiCad's global footprint table
```

In KiCad's symbol chooser each .kicad_sym is one entry, so you see:
RT_C_0402, RT_C_0603, ..., RT_D_TVS, ..., RT_R_0402, ... sorted alphabetically.

## Install (once)
1. Close KiCad.
2. Preferences > Configure Paths: add `RT_LIB` = `C:/Users/{username}/Documents/Kicad/RT_Lib`
   (or do step 3 first, then add the path variable when KiCad opens).
3. Open `%APPDATA%\kicad\10.0\sym-lib-table` in a text editor. Paste the lines from
   `sym-lib-table_RT_Lib.txt` right before the final `)`. Delete any old RT_Resistors /
   RT_Capacitors / RT_Diodes / RT_Inductors / RT_LEDs / RT_Transistors / easyeda2kicad lines.
4. Same for `%APPDATA%\kicad\10.0\fp-lib-table` with `fp-lib-table_RT_Lib.txt`.
5. Open KiCad. All RT_ libraries show up in the chooser.

## Naming
`R_10k_0402`, `C_100nF_0402_16V_X7R`, `L_10uH_0805`, `FB_600R_0603`,
`D_<MPN>_<pkg>`, `DZ_<V>_<pkg>_<power>`, `TVS_<MPN>_<pkg>`, `LED_<color>_<pkg>`, `Q_<MPN>_<pkg>`.
Search the chooser by value, package, voltage, dielectric, MPN or LCSC number.

## On the schematic
Visible: Reference, Value, Spec (size + key rating). Hidden fields: LCSC, MPN, Manufacturer,
JLC_Class, Datasheet, Description. `LCSC` is the field JLC's BOM import and kicad-jlcpcb-tools read.

## Selection rules
1. JLC Basic first, then Preferred (no loading fee).
2. Otherwise the highest-stock Extended part (stock >= 2000). Gap-fill caps capped at 100V,
   pF caps prefer C0G. Check JLC_Class in the catalog: Extended parts add JLC's setup fee.

## Pinouts
Diodes/LEDs: pin 1 = cathode (matches KiCad Diode_SMD / LED_SMD footprints).
SOT-23 MOSFETs 1=G 2=S 3=D, BJTs 1=B 2=E 3=C. Only standard families included.
