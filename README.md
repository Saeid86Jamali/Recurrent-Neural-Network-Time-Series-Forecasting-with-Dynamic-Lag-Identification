# Neural time-series prediction: historical exploratory notebook

[Time series prediction - RNN .ipynb](Time%20series%20prediction%20-%20RNN%20.ipynb)
contains SimpleRNN, dense-network and LSTM examples, a lagged-window constructor,
and a lag-product plot.

## Implemented workflow

The notebook reads `Data.xlsx`, scales the full series to [-1, 1], constructs
25-value windows, randomly assigns 70%/30% of windows to training/test, and trains
each network for 100 epochs with batch size 5. The test partition is also passed
as validation data during training. The plot helper does not return or select a
lag: the actual window length is fixed at 25.

## Reproducibility and interpretation

- `Data.xlsx` is absent, and its source, schema, rights and measurement units are
  not documented. The recorded results cannot currently be reproduced.
- Scaling uses the full series before splitting, and overlapping windows are
  randomly split. This does not constitute a clean chronological forecast test.
- The recurrent input shape is `(samples, 1, 25)`: one recurrent time step with
  25 features, rather than 25 sequential recurrent steps.
- The lag calculation uses uncentered products without variance normalization.
  Its `biased`/`unbiased` denominator labels are reversed relative to the usual
  convention; it should not be described as automatic validated lag selection.
- Later plotting cells hard-code 1,116 test observations. Seeds, an exact
  environment and a separate final test interval are not recorded.

The saved losses are historical outputs, not validated out-of-time forecasting
accuracy. A corrected study needs an authorized dataset, a chronological split,
training-only preprocessing, separate validation/test intervals, explicit tensor
semantics, and comparison with simple forecasting baselines.

## Inspect the original

```bash
jupyter notebook 'Time series prediction - RNN .ipynb'
```

Imports use NumPy, pandas, Keras, scikit-learn and Matplotlib. Jupyter and an Excel
reader compatible with the original pandas version are also needed. The Keras
backend/version and Excel engine were not captured, so no tested installation
command or replacement dataset is asserted.

## Reproducibility status

The original notebook and its saved outputs are retained as historical evidence.
The notebook metadata records Python 3.7.9, but no exact dependency lockfile or
random seed was committed. The original numerical outputs have not been
reproduced by the November 2026 documentation audit. Installing current packages
does not reproduce the historical environment.

This is an exploratory educational example on one dataset. It does not establish
general algorithm superiority or clinical validity. No paper or preprint is
claimed for this repository.

## Attribution and reuse

Repository maintained by Saeid Jamali. The original algorithms and datasets belong
to their respective authors. No license file is present; this documentation
revision does not grant a new software or data license. See Git history for the
original notebook and earlier descriptions.
