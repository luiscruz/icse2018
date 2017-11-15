# ICSE 2018

"On the Energy Footprint of Mobile Testing Frameworks"\\
Paper submitted to the 40th International Conference on Software Engineering (ICSE 2018)

To run experiments:

```
pip install -r requirements.txt
python -m physalia_energy_tests.run
```

To generate reports:

```
python android_test_inspector/reports.py -o <output_dir>
```

Raw data is stored in file `results.csv`.

This work is under double blind review constraints.

You will be able o contact the authors once constraints are lifted.

----

## Rebuttal

We thank the reviewers for their feedback and will adjust our paper to better
explain the issues raised.

### Reproducibility

As requested, we provide our code and collected data in the anonymized site:

https://github.com/esofresearcher/icse2018

Scripts were manually and carefully crafted and peer reviewed to ascertain
similar behavior across all frameworks. We decided not to include UI recorders,
since they rely in the underlying frameworks. These frameworks are designed to
be used with UI descriptors rather than pixel position, favoring compatibility
with different devices and releases.

### Metrics and Normalization


The idea of measuring the idle cost of the app is indeed interesting. In preliminary results, executed during the rebuttal period, we observed that the idle execution consumes 0.0933mW (i.e., mJ/s). For instance, a tap event, after factoring out idle consumption, with the best framework, Espresso, consumes 4.952mJ and with the worst, Appium, 42.606mJ. We noted, however, that the conclusions of our study remain unchanged. We will extend our results section to include duration and energy consumption without idle cost (E), according to the following equation:

E=E_total-Duration*Idle_cost_rate

We don't include energy measurements for human UI interactions. While it may be
feasible for a tap, other interactions (e.g., swipe, drag&drop) are not
trivially factored out from human bias. Energy consumption of a human
interaction consists of the consumption of capacitive sensors, which is
negligible [1], and the events triggered by the system. Since frameworks do not
bypass these events, we adopt a conservative evaluation of results, including
overheads, by using the best framework case as baseline.

### Generalization of results

We studied a self-developed app because to measure energy consumption in a
controlled environment. The app prevents side-effects from UI interactions,
which in real apps would result in different behaviors, hence compromising
measurements. Reported energy consumptions generalize to real apps, given that
frameworks operate similarly regardless of the app under test.


### Implications

We considered the decision tree as being one of the practical contributions of
our work: it aids developers in making an educated guess about the most suited
and energy efficient framework, given the idiosyncrasies of an app (that may
restrict the usage of a framework). As example, Espresso is not compatible with
hybrid apps and Appium should be used in those cases.

Another contribution of this work is to drive a change in the mindset of tool
developers, bringing awareness of the energy consumption of their tools. Thus,
we expect future releases to become more energy efficient. Our results show
that conclusions in previous work (cf. ref [4]) could have been
different if a different framework was used.

### Results Reports

We opt for using violin plots since they provide a visualization of the distribution and comparison of results regarding shape, location, and scale. The fact that p-values were all less than alpha can be verified with the violin plots.


[1] Gao, Shuo, Jackson Lai, and Arokia Nathan. "Fast Readout and Low Power Consumption in Capacitive Touch Screen Panel by Downsampling." Journal of Display Technology (2016):1417-1422.


