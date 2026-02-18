# Extended Filament Profiles

This overlay adds extended filament profiles for Polymaker product lines to the Snapmaker U1 firmware.

## Added Profiles

### Polymaker PLA

- **Panchroma** - New high-speed aesthetic PLA line (standard temp: 220°C, volumetric speed up to 28mm³/s)
- **Panchroma Matte** - Matte finish variant of Panchroma (standard temp: 220°C)
- **PolyLite** - Legacy standard PLA line (standard temp: 220°C) - for backward compatibility
- **PolyTerra** - Legacy eco-friendly PLA line (lower temp: 215°C) - for backward compatibility
- **PolyMax** - Tough PLA line (higher temp: 225°C) - still actively sold

### Polymaker PETG

- **PolyLite** - Standard PETG line (temp: 250°C)
- **PolyMax** - Tough PETG line (temp: 255°C)

### Polymaker ABS

- **PolyLite** - Standard ABS line (temp: 260°C)
- **PolyMax** - Tough ABS line (higher temp: 265°C)

## Technical Details

Each profile includes calibrated parameters for:

- **load_temp** - Temperature for loading filament
- **unload_temp** - Temperature for unloading filament  
- **clean_nozzle_temp** - Temperature for nozzle cleaning
- **flow_temp** - Optimal flow temperature
- **flow_k** - Flow calibration constant
- **flow_k_min/max** - Acceptable flow range
- **is_soft** - Whether filament is flexible

## Usage

### With RFID Tags (OpenSpool Format)

When programming RFID tags, use these values:

```json
{
  "protocol": "openspool",
  "version": "1.0",
  "brand": "Polymaker",
  "type": "PLA",
  "subtype": "Panchroma",
  "color_hex": "FF0000",
  "min_temp": 190,
  "max_temp": 230
}
```

Supported `subtype` values for PLA:
- `Panchroma` - Current product line (recommended)
- `Panchroma Matte` - Matte finish variant
- `PolyLite` - Legacy support
- `PolyTerra` - Legacy support
- `PolyMax` - Still available

### Manual Selection

The profiles will be available in the printer's UI when selecting filament with:
- **Vendor:** Polymaker
- **Type:** PLA, anchroma, Panchroma Matte, PolyLite, PolyTerra, PolyMax

## Product Line Changes

**Note:** Polymaker has consolidated their aesthetic PLA lines under the new **Panchroma™** brand. The previous PolyLite™ PLA and PolyTerra™ PLA color options have been replaced by Panchroma. This overlay includes profiles for both the new Panchroma line and legacy products for backward compatibility with existing RFID tags and user preferences.
- **Sub Type:** PolyTerra, PolyLite, PolyMax, or Panchroma

## Profile Sources

Temperature and flow values are based on:
- Polymaker official filament datasheets
- Community testing and feedback
- Standard Snapmaker U1 calibration ranges

## Extending This Overlay

To add more filament brands or subtypes:

1. Edit the patch file to add new vendor sections following this structure:
   ```python
   'vendor_BrandName': {
       'sub_ProductLine': {
           'load_temp': 250,
           'unload_temp': 250,
           'clean_nozzle_temp': 170,
           'is_soft': False,
           'flow_temp': 220,
           'flow_k': 0.02,
           'flow_slow_v': 0.8,
           'flow_fast_v': 8.0,
           'flow_k_min': 0.012,
           'flow_k_max': 0.028,
       },
   },
   ```

2. Add profiles under the appropriate main types: PLA, PETG, ABS, TPU, etc.

3. Test with actual filament to verify temperatures and flow rates

## References

- [Polymaker Panchroma™ Product Page](https://wiki.polymaker.com/polymaker-products/polymaker-filaments/panchroma-tm)
- [Polymaker Technical Datasheets](https://polymaker.com/downloads/)
- [RFID Support Documentation](../../docs/rfid_support.md)
- [Filament Parameters Source Code](../../tmp/extracted/rootfs/home/lava/klipper/klippy/extras/filament_parameters.py)
