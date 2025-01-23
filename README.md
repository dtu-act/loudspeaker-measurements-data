# Loudspeaker measurement data

This repository holds data from measurements with 5 loudspeakers, see [image](./image) folder:

- `libratone_3inch`: a driver measured in free air
- `bo-encl`: a driver in a closed box
- `huawei-radiator-1`: a low-cost driver in a box with two resonators
- `huawei-vented-1`: a low-cost driver in a vented box
- `purifi`: a hifi driver in free air

The data is available for download under the release page. The `processed.asdf` files can be read in Python as

```python
>>> import asdf
>>> af = asdf.open("processed.asdf")
>>> af["measurements"].info()
[{'amp_ratio': '1-16',
  'bandwidth_fhigh': 500.0,
  'bandwidth_flow': 35.0,
  'bandwidth_fname': 'fr.25-fb.5',
  'breakup_frequency': 1000,
  'initial_dcs_corrected': None,
  'input_data': <array (unloaded) shape: [39995, 4] dtype: float64>,
  'input_data_var': <array (unloaded) shape: [79990, 4] dtype: float64>,
  'input_names': ['voltage', 'current', 'displacement', 'velocity'],
  'input_units': ['V', 'A', 'mm', 'm/s'],
  'mean_var': <array (unloaded) shape: [4] dtype: float64>,
  'measurement_name': 'pinknoise_5s_seed_0_amp_1-16_fr.25-fb.5_253mV.asdf',
  'num_reps': 32,
  'output_data': <array (unloaded) shape: [95990] dtype: float64>,
  'output_name': 'output',
  'output_unit': 'V',
  'post_var': <array (unloaded) shape: [4] dtype: float64>,
  'pre_var': <array (unloaded) shape: [4] dtype: float64>,
  'resonance_frequency': 140,
  'samplerate': 8000,
  'seed': 0,
  'signal': 'pinknoise',
  'vrms': 0.25355939110528053},
  ...]
```

The data consists of measurements of driving voltage, driving current, membrane displacement and membrane velocity. Each measurment is the mean over multiple repetitions ("num_reps") with a mean noise variance estimate `mean_var`.

The measurement name gives an overview of the available data for each driver (except for `purify` which only contains a subset).

```python
>>> [a["measurement_name"] for a in af["measurements"]]
['pinknoise_5s_seed_0_amp_1-16_fr.25-fb.5_253mV.asdf',
 'pinknoise_5s_seed_0_amp_1-1_fr.25-fb.5_4056mV.asdf',
 'pinknoise_5s_seed_0_amp_1-2_fr.25-fb.5_2028mV.asdf',
 'pinknoise_5s_seed_0_amp_1-32_fr.25-fb.5_126mV.asdf',
 'pinknoise_5s_seed_0_amp_1-4_fr.25-fb.5_1014mV.asdf',
 'pinknoise_5s_seed_0_amp_1-8_fr.25-fb.5_507mV.asdf',
 'pinknoise_5s_seed_1_amp_1-16_fr.25-fb.5_253mV.asdf',
 'pinknoise_5s_seed_1_amp_1-1_fr.25-fb.5_4061mV.asdf',
 'pinknoise_5s_seed_1_amp_1-2_fr.25-fb.5_2030mV.asdf',
 'pinknoise_5s_seed_1_amp_1-32_fr.25-fb.5_126mV.asdf',
 'pinknoise_5s_seed_1_amp_1-4_fr.25-fb.5_1015mV.asdf',
 'pinknoise_5s_seed_1_amp_1-8_fr.25-fb.5_507mV.asdf',
 'pinknoise_60s_seed_0_amp_1-1_fr.25-fb.5_4641mV.asdf',
 'pinknoise_60s_seed_1_amp_1-1_fr.25-fb.5_4642mV.asdf',
 'sweep_5s_amp_1-16_fr.25-fb.5_318mV.asdf',
 'sweep_5s_amp_1-1_fr.25-fb.5_5100mV.asdf',
 'sweep_5s_amp_1-2_fr.25-fb.5_2550mV.asdf',
 'sweep_5s_amp_1-32_fr.25-fb.5_159mV.asdf',
 'sweep_5s_amp_1-4_fr.25-fb.5_1275mV.asdf',
 'sweep_5s_amp_1-8_fr.25-fb.5_637mV.asdf']
```

There are 

- 5s pinknoise input at 6 input levels and 2 noise realizations,
- 60s pinknoise input at maximum input level and 2 noise realisations, and
- 5s sweep input at 6 input levels.

All measurements are recorded with a sample rate of 8000 Hz and with an input frequency range of 1/4th the driver's resonance frequency up to 1/2 the frequency of the first driver cone breakup mode.
