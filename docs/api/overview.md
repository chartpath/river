# Overview

## anomaly

Anomaly detection.

The estimators in the `anomaly` module have a slightly different API. Instead of a `predict_one`
method, each anomaly detector has a `score_one`. The latter returns an anomaly score for a given
set of features. High scores indicate anomalies, whereas low scores indicate normal observations.
Note that the range of the scores is relative to each estimator.



- [HalfSpaceTrees](../anomaly/HalfSpaceTrees)

## base

Base interfaces.

Every estimator in `river` is a class, and as such inherits from at least one base interface.
These are used to categorize, organize, and standardize the many estimators that `river`
contains.

This module contains mixin classes, which are all suffixed by `Mixin`. Their purpose is to
provide additional functionality to an estimator, and thus need to be used in conjunction with a
non-mixin base class.

This module also contains utilities for type hinting and tagging estimators.



- [AnomalyDetector](../base/AnomalyDetector)
- [Classifier](../base/Classifier)
- [Clusterer](../base/Clusterer)
- [DriftDetector](../base/DriftDetector)
- [EnsembleMixin](../base/EnsembleMixin)
- [Estimator](../base/Estimator)
- [MiniBatchClassifier](../base/MiniBatchClassifier)
- [MiniBatchRegressor](../base/MiniBatchRegressor)
- [MultiOutputMixin](../base/MultiOutputMixin)
- [Regressor](../base/Regressor)
- [SupervisedTransformer](../base/SupervisedTransformer)
- [Transformer](../base/Transformer)
- [WrapperMixin](../base/WrapperMixin)

## cluster

Unsupervised clustering.

- [KMeans](../cluster/KMeans)

## compat

Compatibility tools.

This module contains adapters for making `river` estimators compatible with other libraries, and
vice-versa whenever possible. The relevant adapters will only be usable if you have installed the
necessary library. For instance, you have to install scikit-learn in order to use the
`compat.convert_sklearn_to_river` function.



**Classes**
- [River2SKLClassifier](../compat/River2SKLClassifier)
- [River2SKLClusterer](../compat/River2SKLClusterer)
- [River2SKLRegressor](../compat/River2SKLRegressor)
- [River2SKLTransformer](../compat/River2SKLTransformer)
- [SKL2RiverClassifier](../compat/SKL2RiverClassifier)
- [SKL2RiverRegressor](../compat/SKL2RiverRegressor)
**Functions**
- [convert_river_to_sklearn](../compat/convert-river-to-sklearn)
- [convert_sklearn_to_river](../compat/convert-sklearn-to-river)

## compose

Model composition.

This module contains utilities for merging multiple modeling steps into a single pipeline. Although
pipelines are not the only way to process a stream of data, we highly encourage you to use them.



- [Discard](../compose/Discard)
- [FuncTransformer](../compose/FuncTransformer)
- [Grouper](../compose/Grouper)
- [Pipeline](../compose/Pipeline)
- [Renamer](../compose/Renamer)
- [Select](../compose/Select)
- [SelectType](../compose/SelectType)
- [TransformerUnion](../compose/TransformerUnion)

## datasets

Datasets.

This module contains a collection of datasets for multiple tasks: classification, regression, etc.
The data corresponds to popular datasets and are conveniently wrapped to easily iterate over
the data in a stream fashion. All datasets have fixed size. Please refer to `river.synth` if you
are interested in infinite synthetic data generators.



- [AirlinePassengers](../datasets/AirlinePassengers)
- [Bananas](../datasets/Bananas)
- [Bikes](../datasets/Bikes)
- [ChickWeights](../datasets/ChickWeights)
- [CreditCard](../datasets/CreditCard)
- [Elec2](../datasets/Elec2)
- [HTTP](../datasets/HTTP)
- [Higgs](../datasets/Higgs)
- [ImageSegments](../datasets/ImageSegments)
- [Insects](../datasets/Insects)
- [MaliciousURL](../datasets/MaliciousURL)
- [MovieLens100K](../datasets/MovieLens100K)
- [Music](../datasets/Music)
- [Phishing](../datasets/Phishing)
- [Restaurants](../datasets/Restaurants)
- [SMSSpam](../datasets/SMSSpam)
- [SMTP](../datasets/SMTP)
- [SolarFlare](../datasets/SolarFlare)
- [TREC07](../datasets/TREC07)
- [Taxis](../datasets/Taxis)
- [TrumpApproval](../datasets/TrumpApproval)

## drift


Concept Drift Detection.

This module contains concept drift detection methods. The purpose of a drift detector is to raise
an alarm if the data distribution changes. A good drift detector method is the one that maximizes
the true positives while keeping the number of false positives to a minimum.



- [ADWIN](../drift/ADWIN)
- [DDM](../drift/DDM)
- [EDDM](../drift/EDDM)
- [HDDM_A](../drift/HDDM-A)
- [HDDM_W](../drift/HDDM-W)
- [KSWIN](../drift/KSWIN)
- [PageHinkley](../drift/PageHinkley)

## dummy

Dummy estimators.

This module is here for testing purposes, as well as providing baseline performances.



- [NoChangeClassifier](../dummy/NoChangeClassifier)
- [PriorClassifier](../dummy/PriorClassifier)
- [StatisticRegressor](../dummy/StatisticRegressor)

## ensemble

Ensemble learning.

This module includes ensemble methods. This kind of methods improve predictive performance by
combining the prediction of their members.



- [ADWINBaggingClassifier](../ensemble/ADWINBaggingClassifier)
- [AdaBoostClassifier](../ensemble/AdaBoostClassifier)
- [AdaptiveRandomForestClassifier](../ensemble/AdaptiveRandomForestClassifier)
- [AdaptiveRandomForestRegressor](../ensemble/AdaptiveRandomForestRegressor)
- [BaggingClassifier](../ensemble/BaggingClassifier)
- [BaggingRegressor](../ensemble/BaggingRegressor)
- [LeveragingBaggingClassifier](../ensemble/LeveragingBaggingClassifier)
- [SRPClassifier](../ensemble/SRPClassifier)

## evaluate

Model evaluation.



- [progressive_val_score](../evaluate/progressive-val-score)

## expert

Expert learning.

This module regroups a variety of methods that may be used for performing model selection. An
expert learner is provided with a list of models, which are also called experts, and is tasked with
performing at least as well as the best expert. Indeed, initially the best model is not known. The
performance of each model becomes more apparent as time goes by. Different strategies are possible,
each one offering a different tradeoff in terms of accuracy and computational performance.

Expert learning can be used for tuning the hyperparameters of a model. This may be done by creating
a copy of the model for each set of hyperparameters, and treating each copy as a separate model.
The `utils.expand_param_grid` function can be used for this purpose.

Note that this differs from the `ensemble` module in that methods from the latter are designed to
improve the performance of a single model. Both modules may thus be used in conjunction with one
another.



- [EWARegressor](../expert/EWARegressor)
- [StackingClassifier](../expert/StackingClassifier)
- [SuccessiveHalvingClassifier](../expert/SuccessiveHalvingClassifier)
- [SuccessiveHalvingRegressor](../expert/SuccessiveHalvingRegressor)

## facto

Factorization machines.

- [FFMClassifier](../facto/FFMClassifier)
- [FFMRegressor](../facto/FFMRegressor)
- [FMClassifier](../facto/FMClassifier)
- [FMRegressor](../facto/FMRegressor)
- [FwFMClassifier](../facto/FwFMClassifier)
- [FwFMRegressor](../facto/FwFMRegressor)
- [HOFMClassifier](../facto/HOFMClassifier)
- [HOFMRegressor](../facto/HOFMRegressor)

## feature_extraction

Feature extraction.

This module can be used to extract information from raw features. This includes encoding
categorical data as well as looking at interactions between existing features. This differs from
the `processing` module in that the latter's purpose is rather to clean the data so that it may
be processed by a particular machine learning algorithm.



- [Agg](../feature-extraction/Agg)
- [BagOfWords](../feature-extraction/BagOfWords)
- [PolynomialExtender](../feature-extraction/PolynomialExtender)
- [RBFSampler](../feature-extraction/RBFSampler)
- [TFIDF](../feature-extraction/TFIDF)
- [TargetAgg](../feature-extraction/TargetAgg)

## feature_selection

Feature selection.

- [PoissonInclusion](../feature-selection/PoissonInclusion)
- [SelectKBest](../feature-selection/SelectKBest)
- [VarianceThreshold](../feature-selection/VarianceThreshold)

## imblearn

Sampling methods.

- [HardSamplingClassifier](../imblearn/HardSamplingClassifier)
- [HardSamplingRegressor](../imblearn/HardSamplingRegressor)
- [RandomOverSampler](../imblearn/RandomOverSampler)
- [RandomSampler](../imblearn/RandomSampler)
- [RandomUnderSampler](../imblearn/RandomUnderSampler)

## linear_model

Linear models.

- [ALMAClassifier](../linear-model/ALMAClassifier)
- [LinearRegression](../linear-model/LinearRegression)
- [LogisticRegression](../linear-model/LogisticRegression)
- [PAClassifier](../linear-model/PAClassifier)
- [PARegressor](../linear-model/PARegressor)
- [Perceptron](../linear-model/Perceptron)
- [SoftmaxRegression](../linear-model/SoftmaxRegression)

## meta

Meta-models.

- [BoxCoxRegressor](../meta/BoxCoxRegressor)
- [PredClipper](../meta/PredClipper)
- [TransformedTargetRegressor](../meta/TransformedTargetRegressor)

## metrics

Evaluation metrics.

All the metrics are updated one sample at a time. This way we can track performance of
predictive methods over time.



- [Accuracy](../metrics/Accuracy)
- [BalancedAccuracy](../metrics/BalancedAccuracy)
- [ClassificationReport](../metrics/ClassificationReport)
- [CohenKappa](../metrics/CohenKappa)
- [ConfusionMatrix](../metrics/ConfusionMatrix)
- [CrossEntropy](../metrics/CrossEntropy)
- [ExactMatch](../metrics/ExactMatch)
- [ExampleF1](../metrics/ExampleF1)
- [ExampleFBeta](../metrics/ExampleFBeta)
- [ExamplePrecision](../metrics/ExamplePrecision)
- [ExampleRecall](../metrics/ExampleRecall)
- [F1](../metrics/F1)
- [FBeta](../metrics/FBeta)
- [GeometricMean](../metrics/GeometricMean)
- [Hamming](../metrics/Hamming)
- [HammingLoss](../metrics/HammingLoss)
- [Jaccard](../metrics/Jaccard)
- [KappaM](../metrics/KappaM)
- [KappaT](../metrics/KappaT)
- [LogLoss](../metrics/LogLoss)
- [MAE](../metrics/MAE)
- [MCC](../metrics/MCC)
- [MSE](../metrics/MSE)
- [MacroF1](../metrics/MacroF1)
- [MacroFBeta](../metrics/MacroFBeta)
- [MacroPrecision](../metrics/MacroPrecision)
- [MacroRecall](../metrics/MacroRecall)
- [Metric](../metrics/Metric)
- [MicroF1](../metrics/MicroF1)
- [MicroFBeta](../metrics/MicroFBeta)
- [MicroPrecision](../metrics/MicroPrecision)
- [MicroRecall](../metrics/MicroRecall)
- [MultiFBeta](../metrics/MultiFBeta)
- [Precision](../metrics/Precision)
- [R2](../metrics/R2)
- [RMSE](../metrics/RMSE)
- [RMSLE](../metrics/RMSLE)
- [ROCAUC](../metrics/ROCAUC)
- [Recall](../metrics/Recall)
- [RegressionMultiOutput](../metrics/RegressionMultiOutput)
- [Rolling](../metrics/Rolling)
- [SMAPE](../metrics/SMAPE)
- [TimeRolling](../metrics/TimeRolling)
- [WeightedF1](../metrics/WeightedF1)
- [WeightedFBeta](../metrics/WeightedFBeta)
- [WeightedPrecision](../metrics/WeightedPrecision)
- [WeightedRecall](../metrics/WeightedRecall)

## multiclass

Multi-class classification.

- [OneVsOneClassifier](../multiclass/OneVsOneClassifier)
- [OneVsRestClassifier](../multiclass/OneVsRestClassifier)
- [OutputCodeClassifier](../multiclass/OutputCodeClassifier)

## multioutput

Multi-output models.

- [ClassifierChain](../multioutput/ClassifierChain)
- [MonteCarloClassifierChain](../multioutput/MonteCarloClassifierChain)
- [ProbabilisticClassifierChain](../multioutput/ProbabilisticClassifierChain)
- [RegressorChain](../multioutput/RegressorChain)

## naive_bayes

Naive Bayes algorithms.

- [BernoulliNB](../naive-bayes/BernoulliNB)
- [ComplementNB](../naive-bayes/ComplementNB)
- [GaussianNB](../naive-bayes/GaussianNB)
- [MultinomialNB](../naive-bayes/MultinomialNB)

## neighbors

Neighbors-based learning.

Also known as *lazy* methods. In these methods, generalisation of the training data is delayed
until a query is received.



- [KNNADWINClassifier](../neighbors/KNNADWINClassifier)
- [KNNClassifier](../neighbors/KNNClassifier)
- [KNNRegressor](../neighbors/KNNRegressor)
- [SAMKNNClassifier](../neighbors/SAMKNNClassifier)

## optim

Stochastic optimization.

- [AMSGrad](../optim/AMSGrad)
- [AdaBound](../optim/AdaBound)
- [AdaDelta](../optim/AdaDelta)
- [AdaGrad](../optim/AdaGrad)
- [AdaMax](../optim/AdaMax)
- [Adam](../optim/Adam)
- [Averager](../optim/Averager)
- [FTRLProximal](../optim/FTRLProximal)
- [Momentum](../optim/Momentum)
- [Nadam](../optim/Nadam)
- [NesterovMomentum](../optim/NesterovMomentum)
- [Optimizer](../optim/Optimizer)
- [RMSProp](../optim/RMSProp)
- [SGD](../optim/SGD)
### initializers

Weight initializers.

- [Constant](../optim/initializers/Constant)
- [Normal](../optim/initializers/Normal)
- [Zeros](../optim/initializers/Zeros)

### losses

Loss functions.

Each loss function is intended to work with both single values as well as numpy vectors.



- [Absolute](../optim/losses/Absolute)
- [BinaryFocalLoss](../optim/losses/BinaryFocalLoss)
- [BinaryLoss](../optim/losses/BinaryLoss)
- [Cauchy](../optim/losses/Cauchy)
- [CrossEntropy](../optim/losses/CrossEntropy)
- [EpsilonInsensitiveHinge](../optim/losses/EpsilonInsensitiveHinge)
- [Hinge](../optim/losses/Hinge)
- [Log](../optim/losses/Log)
- [MultiClassLoss](../optim/losses/MultiClassLoss)
- [Poisson](../optim/losses/Poisson)
- [Quantile](../optim/losses/Quantile)
- [RegressionLoss](../optim/losses/RegressionLoss)
- [Squared](../optim/losses/Squared)

### schedulers

Learning rate schedulers.

- [Constant](../optim/schedulers/Constant)
- [InverseScaling](../optim/schedulers/InverseScaling)
- [Optimal](../optim/schedulers/Optimal)
- [Scheduler](../optim/schedulers/Scheduler)


## preprocessing

Feature preprocessing.

The purpose of this module is to modify an existing set of features so that they can be processed
by a machine learning algorithm. This may be done by scaling numeric parts of the data or by
one-hot encoding categorical features. The difference with the `feature_extraction` module is that
the latter extracts new information from the data



- [Binarizer](../preprocessing/Binarizer)
- [FeatureHasher](../preprocessing/FeatureHasher)
- [LDA](../preprocessing/LDA)
- [MaxAbsScaler](../preprocessing/MaxAbsScaler)
- [MinMaxScaler](../preprocessing/MinMaxScaler)
- [Normalizer](../preprocessing/Normalizer)
- [OneHotEncoder](../preprocessing/OneHotEncoder)
- [RobustScaler](../preprocessing/RobustScaler)
- [StandardScaler](../preprocessing/StandardScaler)

## proba

Probability distributions.

- [Gaussian](../proba/Gaussian)
- [Multinomial](../proba/Multinomial)

## reco

Recommender systems.

- [Baseline](../reco/Baseline)
- [BiasedMF](../reco/BiasedMF)
- [FunkMF](../reco/FunkMF)
- [RandomNormal](../reco/RandomNormal)

## stats

Running statistics

- [AbsMax](../stats/AbsMax)
- [AutoCorr](../stats/AutoCorr)
- [BayesianMean](../stats/BayesianMean)
- [Bivariate](../stats/Bivariate)
- [Count](../stats/Count)
- [Cov](../stats/Cov)
- [EWMean](../stats/EWMean)
- [EWVar](../stats/EWVar)
- [Entropy](../stats/Entropy)
- [IQR](../stats/IQR)
- [Kurtosis](../stats/Kurtosis)
- [Link](../stats/Link)
- [Max](../stats/Max)
- [Mean](../stats/Mean)
- [Min](../stats/Min)
- [Mode](../stats/Mode)
- [NUnique](../stats/NUnique)
- [PeakToPeak](../stats/PeakToPeak)
- [PearsonCorr](../stats/PearsonCorr)
- [Quantile](../stats/Quantile)
- [RollingAbsMax](../stats/RollingAbsMax)
- [RollingCov](../stats/RollingCov)
- [RollingIQR](../stats/RollingIQR)
- [RollingMax](../stats/RollingMax)
- [RollingMean](../stats/RollingMean)
- [RollingMin](../stats/RollingMin)
- [RollingMode](../stats/RollingMode)
- [RollingPeakToPeak](../stats/RollingPeakToPeak)
- [RollingPearsonCorr](../stats/RollingPearsonCorr)
- [RollingQuantile](../stats/RollingQuantile)
- [RollingSEM](../stats/RollingSEM)
- [RollingSum](../stats/RollingSum)
- [RollingVar](../stats/RollingVar)
- [SEM](../stats/SEM)
- [Shift](../stats/Shift)
- [Skew](../stats/Skew)
- [Sum](../stats/Sum)
- [Univariate](../stats/Univariate)
- [Var](../stats/Var)

## stream

Streaming utilities.

The module includes tools to iterate over data streams.



**Classes**
- [Cache](../stream/Cache)
**Functions**
- [iter_arff](../stream/iter-arff)
- [iter_array](../stream/iter-array)
- [iter_csv](../stream/iter-csv)
- [iter_libsvm](../stream/iter-libsvm)
- [iter_pandas](../stream/iter-pandas)
- [iter_sklearn_dataset](../stream/iter-sklearn-dataset)
- [shuffle](../stream/shuffle)
- [simulate_qa](../stream/simulate-qa)

## synth

Synthetic datasets.

Each synthetic dataset is a stream generator. The benefit of using a generator is that they do not
store the data and each data sample is generated on the fly. Except for a couple of methods,
the majority of these methods are infinite data generators.



- [Agrawal](../synth/Agrawal)
- [AnomalySine](../synth/AnomalySine)
- [ConceptDriftStream](../synth/ConceptDriftStream)
- [Friedman](../synth/Friedman)
- [Hyperplane](../synth/Hyperplane)
- [LED](../synth/LED)
- [LEDDrift](../synth/LEDDrift)
- [Logical](../synth/Logical)
- [Mixed](../synth/Mixed)
- [RandomRBF](../synth/RandomRBF)
- [RandomRBFDrift](../synth/RandomRBFDrift)
- [RandomTree](../synth/RandomTree)
- [SEA](../synth/SEA)
- [STAGGER](../synth/STAGGER)
- [Sine](../synth/Sine)
- [Waveform](../synth/Waveform)

## time_series

Time series forecasting.

- [Detrender](../time-series/Detrender)
- [GroupDetrender](../time-series/GroupDetrender)
- [SNARIMAX](../time-series/SNARIMAX)

## tree

Tree-based methods.

This modules contains tree-based methods. Similar to the batch learning versions, these methods
model data by means of a tree-structure. However, these methods create the tree incrementally.



- [BaseHoeffdingTree](../tree/BaseHoeffdingTree)
- [ExtremelyFastDecisionTreeClassifier](../tree/ExtremelyFastDecisionTreeClassifier)
- [HoeffdingAdaptiveTreeClassifier](../tree/HoeffdingAdaptiveTreeClassifier)
- [HoeffdingAdaptiveTreeRegressor](../tree/HoeffdingAdaptiveTreeRegressor)
- [HoeffdingTreeClassifier](../tree/HoeffdingTreeClassifier)
- [HoeffdingTreeRegressor](../tree/HoeffdingTreeRegressor)
- [LabelCombinationHoeffdingTreeClassifier](../tree/LabelCombinationHoeffdingTreeClassifier)
- [iSOUPTreeRegressor](../tree/iSOUPTreeRegressor)

## utils

Utility classes and functions.

**Classes**
- [Histogram](../utils/Histogram)
- [SDFT](../utils/SDFT)
- [Skyline](../utils/Skyline)
- [SortedWindow](../utils/SortedWindow)
- [VectorDict](../utils/VectorDict)
- [Window](../utils/Window)
**Functions**
- [check_estimator](../utils/check-estimator)
- [dict2numpy](../utils/dict2numpy)
- [expand_param_grid](../utils/expand-param-grid)
- [numpy2dict](../utils/numpy2dict)
### math

Mathematical utility functions (intended for internal purposes).

A lot of this is experimental and has a high probability of changing in the future.



- [chain_dot](../utils/math/chain-dot)
- [clamp](../utils/math/clamp)
- [dot](../utils/math/dot)
- [dotvecmat](../utils/math/dotvecmat)
- [matmul2d](../utils/math/matmul2d)
- [minkowski_distance](../utils/math/minkowski-distance)
- [norm](../utils/math/norm)
- [outer](../utils/math/outer)
- [prod](../utils/math/prod)
- [sherman_morrison](../utils/math/sherman-morrison)
- [sigmoid](../utils/math/sigmoid)
- [sign](../utils/math/sign)
- [softmax](../utils/math/softmax)

### pretty

Helper functions for making things readable by humans.

- [humanize_bytes](../utils/pretty/humanize-bytes)
- [print_table](../utils/pretty/print-table)


