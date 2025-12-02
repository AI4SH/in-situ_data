# AI4SoilHelath in-situ data

The [EU Soil Mission][EUSoilMission] supported project [AI4SoilHealth][AI4SH] includes a component ("work-package") on in-situ soil sampling. In total 13 different methods were tested for in-situ data sampling and analysis. Links to documentation and data for the different methods are available in the left panel and under the short description of each method on this page.

## Data access and organisation

The data is provided under the following licenses:

- Data License: Creative Commons Attribution license (**CC-BY**)
- Code License: Massachusetts Institute of Technology License ()**MIT License**)

All data is supplied in two different version with different organisation:

-  flat json object database (ore suitable for direct accessibility), and
-  nested json object databas (better for converting to sql database).

The the data is found under separate sub-folders under the _flat_ and _nested_ folders. More detailed information on each method is available on the [documentation][https://ai4sh.github.io/in-situ_data_docs/docs/] site. There each method, including expalined examples of the json data is oulined in more detail. Furhter down this README file contains a summary of each method, with links to the respective documentation pages.

### Json objects

The json objects are the same in both the _flat_ and _nested_ data formats, here illustrated with a _flat_ json data file.

```
{
  "campaign": "ai4sh_fi-jokioinen", # 'project'+'_'+'country'+'-'+'pilot site'
  "sampling_log": { # Assembly of samples collected in the same day at a particular pilot site
    "name": "fi-jokioinen-20241008", # 'country'+'-'+'pilot site'+'-'+'sampling date'
    "date_stamp": "20241008", # Date when the sample was collected in the field
    "person__email": "thomasg@xspectre.com" # Email of person responsible for the sampling
  },
  "sample": "fi-jokioinen-20241008_7-r_0-20", # 'country'+'-'+'pilot site'+'-'+'sampling date'+'_'+'sample point id'+'_'+'min depth''+'-'+'max depth'
  "locus": { # Assembly of the point location, setting and depth
    "position__name": "fi-jokioinen_7-r", # 'country'+'-'+'pilot site'+'-'+'sample point id' used for checking internal consistency
    "point": "7-r", # sample point id
    "setting": "uniform", # The spatial setting in the landscape (uniform, alley, plantline, edge)
    "latitude": 60.817951078, # Latitude in WGS84
    "longitude": 23.493872667, # Longitude in WGS84
    "min_depth": 0, # Sample upper limit in cm in soil profile
    "max_depth": 20 # Sample lower limit in cm in soil profile
  },
  "observation": { # Assembly of metadata and data related to the observation
    "sample_preparation__name": "soil-undisturbed-in-situ", # Explanatory name of soil treatment before observation
    "person__email": "thomasg@xspectre.com", # Email of person responsible for the observation
    "subsample": "a", # For registering if physically different soil subsamples were analysed separately, default for a single analysis = a
    "replicate": 0, # If the analysis was replicated on the same subsample more than once, the first test is always set to 0
    "n_repeats": 6, # The number of repetitions done by any instrument on a single subsample and as part of a single replicate, with results reported as mean or mean and standard deviation
    "date_stamp": "20241011", # Date when the analysis was done
    "logistic": { # Assembly of logistical metadata on the handling of the sample
      "sample_preservation__name": null, # Explanatory name of soil preservation
      "sample_transport__name": null, # Explanatory name of soil transportation if sensitive for analysis results
      "transport_duration_h": 0, # duration of any sensitive transportation in hours
      "sample_storage__name": null, # Explanatory name of soil storage if sensitive for analysis results
      "storage_duration_h": 72,
      "person__email": "thomasg@xspectre.com" # Email of person responsible for the logistics
    },
    "analysis": {  # Assembly of analysis results, procedures and instruments
      "xspectre-ise-ph-solid_ph(soil)": {  # Soil property reported as AI4SH extended naming (part after underscore = core indicator)
        "value": 6.810666666666665, # Recorded value (single value or mean of repeated observations)
        "standard_deviation": 0.05562573345334154, # Recorded standard deviation of repeated measurements
        "unit__name": "pH", # Recorded unit
        "indicator__name": "xspectre-ise-ph-solid_ph(soil)", # AI4SH extended name of the soil indicator (part after underscore = core indicator)
        "procedure": "xspectre-ise-ph-solid", # Procedure for the analysis
        "analysis_method__name": "ise-ph-soil", # Name of the method
        "instrument_brand__name": "soil-ise-ph", # Instrument type or brand
        "instrument_model__name": "ise-ph-soil", # Model or version of the instrument
        "instrument_id": "0"  # Any individual instrument id, the default for unknown id is "0"
      }
    }
  }
}
```
The _standard deviation_ object only exists for methods that do repeated measurements in each observation and report it. For the spectrometer, the _value_ and _standard deviation_ objects are arrays, for all other methods these are single number objects.

### Difference between subsample, replicate and repetition

The difference between a subsample and a replicate is that if the same physical volume of soil is used for the analysis it is a replicate, but if the analysis is used on a separate physical volume it is a subsample. Thus all destructive analysis methods can per definition not be replicates. repetions (_n_repeats_) refer to the number of scans the insturment performs with each observation. Instruments supplied by the Swedish startup [Xspectre][xspectre] (salinity, pH ISE, penetrometer and 2 different spectrometers) by default run 6 scans and report the results as mean and standard deviation.

## Sample sites

The AI4SH test, or pilot, sites cover many of Europe's agroecological and climate zones and include the following countries:

- Croatia,
- Denmark,
- England,
- Finland,
- France,
- (Germany),
- Greece,
- (Italy),
- Netherlands,
- Spain,
- Sweden,
- Switzerland, and
- Wales.

The pilot sites in Germany and Italy did no include any in-situ data sampling and are thus not covered in this documentation.

## In-situ methods applied

The methods applied for the in-situ data collection within AI4SH can broadly be divided into 3 categories:

1. Professional laboratory methods,
2. Citizen scientist methods, and
3. Direct layperson methods.

### Professional laboratory methods

For all in-situ sites traditional, or "wet", chemicophysical laboratory methods were used as a reference frame for evaluating the suite of alternative and novel methods tested. Most of the collected samples were analysed at the same laboratory, applying the same method for all samples. Only the initial test-sampling at the Greece site Ktima-Gerovassiliou, was not analysed using the same laboratory.

Details on the wet laboratory methods and links to the source data are found in the [wet laboratory][wetlab] folder.

### environmental DNA (eDNA)

Environmental DNA (eDNA) is revolutionising the study of the soil microcosm, both the (groups of) species that exist, and the functions they perform. In soil, eDNA originate mainly from prokaryotes (bacteria and archaea), fungi, protists, plants and animals. The composition of DNA offers a snapshot of ecosystem diversity, function and health. The focus of the eDNA studies in AI4SH is on prokaryotes and fungi.

Details on the eDNA methods and links to the source data are found in the [eDNA][edna] folder.

### Laboratory spectroscopy

Spectroscopy, the study of how electromagnetic radiation interacts with matter, is available not only as a laboratory method; it can also be used by citizen scientists and even as a direct layperson method. In AI4Sh all three levels where tested.

Laboratory spectrometry covers a larger spectral range, bridging from visible (VIS) via near infra-red (NIR) to mid-infrared (MIR) regions. Laboratory spectrometers also have higher spectral resolution and better precision. All samples collected within AI4SH were analysed with a a laboratory spectrometer at 0.5 nano-meter (nm) spectral resolution and covering the range 400 - 2500 nm (full VIS-NIR range). Soil attributes that can be estimated from the full VIS-NIR spectroscopy include for instance carbon, nitrogen and particle size distributions.

Details on the spectroscopy methods and links to the source data are found in the [spectroscopy][spectroscopy] folder.   

## Citizen scientist methods

The citizen scientist methods range from advanced enzymatic analysis using spectroscopy and image analysis to a free app for determining soil aggregate stability. The common denominator for the citizen science methods is that samples need to brought home, prepared and then analysed. But the whole process can be performed in for example a kitchen.

### Soil Enzymatic Activity Reader (SEAR)

SEAR is a method developed by the Swiss startup [DigitSoil][digitsoil-home], a partner in the AI4SH project. In the SEAR method, fresh soil is placed on a reaction plate with 25 cells prepared for identifying 5 different key soil metabolic enzymes. Using built-in spectral analysis, the activity rate for each enzyme is reported in under an hour.

Details on the Digit Soil SEAR method and links to the source data are found in the [enzymatic activity][digitsoil] folder.

### Microbiometer

[Microbiometer][microbiometer-home] is a commercially available kit for analysing soil microorganism carbon content and the ratio between bacteria:fungi. It requires a small soil sample (1 ml) and addition of a reactant that is stirred with the soil sample and then analysed using a reference plate and a smartphone app after 20 minutes. The results are presented immediately.

Details on Microbiometer method and links to the source data are found in the [Microbiometer][microbiometer] folder.

### Aggregate stability (Slakes/Moulder apps)

Aggregate stability - clumps of soil particles held together as a result of biological (i.e. enzymatic) activity is well known for having beneficial effects on soil health. [The Soil Health Institute][soilhealthinstitute] developed the conceptual idea of soaking pie-sized dried soil aggregates in water and estimate stability from the disintegration of the soaked aggregate. University of Sydney developed this into a smartphone app that is freely applicable as a citizen scientist method for estimating soil aggregate stability. The app exists in 2 version, Slakes and Moulder, both available for Apple and Android smartphones. Within AI4SH, the method was tested on subsets of samples for some of the pilot sites.

Details on the Slakes/Moulder app method and links to the source data are found in the [aggregate stability][aggregates] folder.

### Citizen scientist spectroscopy

Spectral instrument that can be used either directly in the field or in a home environment have developed rapidly over the past decade. The commercially available, better range of these instruments are suitable for soil spectroscopy. Ideally, the soil should be dried and sieved before analysis. This eliminates the nonlinear influence of water, and also the soil spectral reference libraries used for estimating soil attributes from the spectra typically are based on dried and sieved samples. Within AI4SH the handheld Neospectra scanner developed by [SI-ware][si-ware], sold to [Buchi][buchi_neospectra] in 2025 and rebranded [ProxiScout][proxiscout] was applied in a majority of the pilot sites. Most samples were analysed both in fresh (wet) conditions, and after drying and sieving.

Details on the NeoSpectra/ProxiScout spectral method and links to the source data are found in the [spectroscopy][spectroscopy] folder.

### Bulk density and soil moisture content

Soil compaction is one of the most serious threats to soil health. Many attempts have been made to quickly estimate bulk density, a proxy for soil compaction, in the field. Hitherto, to our knowledge, no successful direct field method has been presented. Instead a soil cylinder, with a very precise volume, is hammered into the soil with both ends open, then shaved at the openings and dried at 105<sup>o</sup> C. The net dry weight divided by the volume represents the bulk density. By measuring the weight loss over the drying, the method also produces an estimate of soil water content.

Details on the bulk density soil cylinder method and links to the source data are found in the [bulk density and soil moisture content][bulkdensity] folder.

### Ion Selective Electrode (ISE)

Ion selective electrodes are precision instruments used in laboratories. They measure the electrical potential over a membrane with a reference liquid on one side (the probe inside) and a (usually liquid) sample on the other. ISEs exist for many ions but pH ISEs are the most widely used. In the AI4SH project two kinds of pH ISEs were tested, one for direct soil analysis in the field, and one laboratory ISE analysis after dissolving the soil in distilled water at a ratio 1:5.

 Details on the pH Ion Selective Electrode method and links to the source data are found in the [pH ISE][ise] folder.

### Electrical conductivity

Electrical conductivity (EC) is an indication of salinity. Salinity is recognised as one of the major drivers of soil deterioration and a key soil health indicator identified for Europe. EC instruments based on the same technology as ISEs are available on the market, but where not tested. Instead the AI4SH in-situ studies included a simpler bi-pin electronic device measuring the resistance in a soil:water solution of 1:5. The tests where performed on soil brought to an indoor environment but using wet soils without prior drying.

Details on the bi-pin electrical conductivity method and links to the source data are found in the [bi-pin salinity][salinity] folder.


## Direct layperson methods

A plethora of different layperson methods for estimating soil health does exists, including burying pure cotton knickers over a prolonged period; the spade test for sensory examination of wetness, colour, odour, structure, and texture; or measuring the diurnal temperature cycle. In AI4SH the selection of direct layperson methods was restricted to methods that can be applied instantly and that generate a signal without requiring human interpretation of the raw data.

### Layperson spectroscopy

Miniaturisation and technical developments have led to several manufacturers of optical spectra sensors to develop integrated sensing units for combination with microcontrollers. As part of AI4SH we tested two miniature sensors from [Hamamatsu][hamamatsu] built into a casing about the size of a deck of cards and operated either via a computer or a bluetooth connected smartphone. The two selected sensors cover limited spectral ranges in the VIS and short NIR regions. These instruments were tested at a subset of the pilot sites, in most cases scanning both wet and dried and sieved samples. The layperson spectrometers tested in AI4SH were built by the Swedish startup [Xspectre][xspectre].

Details on the Xspectre spectral method and links to the source data are found in the [spectroscopy][spectroscopy] folder.

### Penetrometer

A penetrometer is an instrument with 1 or more spikes of typically 5 to 10 cm length that is pushed into the soil directly in the field. Traditional penetrometers are analogue instruments used for evaluaing soil compaction, but more recent developments have led to small digital penetrometers that can observe a range of soil properties. Connected to a microcontroller and with a power supply of 5 V or more, these instruments can estimate soil moisture, electrical conductivity, salinity, pH and key nutrients. Laboratory tests show that they are capable of giving consistent, but sometimes biased, signals. Penetrometers were applied at a subset of the pilot sites. In AI4SH we tested a 5-pin penetrometer built with an interface developed by the Swedish startup [Xspectre][xspectre].

Details on the Xspectre penetrometer method and links to the source data are found in the [penetrometer][penetrometer] folder.

### Infiltration and soil hydraulic properties

Soil infiltration capacity and other hydraulic properties including water holding capacity, are important properties that relate to flood, drought and erosion risks. A simple method for estimating these hydraulic properties is to insert a small (5-10 cm) cylinder with both ends open a few centimetres into the soil and then repeatedly pour a small fixed volume of water into the cylinder. From the time it takes for the soil to swallow the water, and its change with each sequential fill, the hydraulic properties can be estimated. A prerequisite is that the bulk density and initial and final soil moisture are known. These prerequisites, however, can be obtained with the above listed [penetrometer] instrument and a [soil cylinder][bulkdensity]. The single ring infiltration test was performed at a subset of the pilot site.

Details on the infiltration method and links to the source data are found in the [infiltration][infiltration] folder.

## Acknowledgments and Funding

This work is part of the AI4SoilHealth project, funded by the European Union's Horizon Europe Research and Innovation Programme under Grant Agreement No. 101086179.

_Funded by the European Union. The views expressed are those of the authors and do not necessarily reflect those of the European Union or the European Research Executive Agency._

[AI4SH]: https://ai4soilhealth.eu

[buchi_neospectra]: https://www.walderwyss.com/en/news/2025-05-19_buchi-acquires-neospectra-platform-from-si-ware-systems

[digitsoil-home]: https://www.digit-soil.com

[EUSoilMission]: https://mission-soil-platform.ec.europa.eu

[hamamatsu]: https://www.hamamatsu.com/jp/en/product/optical-sensors/spectrometers/mini-spectrometer.html

[microbiometer-home]: https://microbiometer.com

[proxiscout]:https://www.buchi.com/en/products/instruments/proxiscout

[si-ware]: https://www.si-ware.com

[soilhealthinstitute]: https://soilhealthinstitute.org/our-work/initiatives/slakes/

[xspectre]: https://xspectre.com

[aggregates]: ../docs/in-situ_methods/aggregates/

[bulkdensity]: ../docs/in-situ_methods/bulkdensity/

[edna]: ../docs/in-situ_methods/edna/

[digitsoil]: ../docs/in-situ_methods/digitsoil

[spectroscopy]: ../docs/in-situ_methods/spectroscopy/

[infiltration]: ../docs/in-situ_methods/infiltration

[ise]: ../docs/in-situ_methods/ise/

[microbiometer]: ../docs/in-situ_methods/microbiometer/

[penetrometer]: ../docs/in-situ_methods/penetrometer/

[salinity]: ../docs/in-situ_methods/salinity/

[spectroscopy]: ../docs/in-situ_methods/spectroscopy

[wetlab]: ../docs/in-situ_methods/wetlab/

[in-situ_data]: https://github.com/AI4SH/in-situ_data
