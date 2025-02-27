Dataset features
===========================

:class:`nlp.Features` define the internal structure and typings for each example in the dataset. Features are used to specify the underlying serailization format but also contain high-level informations regarding the fields, e.g. conversion methods from names to integer values for a class label field.

Here is a brief presentation of the various types of features which can be used to define the dataset fields (aka columns):

- :class:`nlp.Features` is the base class and should be only called once and instantiated with a dictionnary of field names and field sub-features as detailed in the rest of this list,
- a python :obj:`dict` specifies that the field is a nested field containing a mapping of sub-fields to sub-fields features. It's possible to have nested fields of nested fields in an arbitrary manner.
- a python :obj:`list` or a :class:`nlp.Sequence` specifies that the field contains a list of objects. The python :obj:`list` or :class:`nlp.Sequence` should be provided with a single sub-feature as an example of the feature type hosted in this list. Python :obj:`list` are simplest to define and write while :class:`nlp.Sequence` provide a few more specific behaviors like the possibility to specify a fixed length for the list (slightly more efficient).

.. note::

	A :class:`nlp.Sequence` with a internal dictionnary feature will be automatically converted in a dictionnary of lists. This behavior is implemented to have a compatilbity layer with the TensorFlow Datasets library but may be un-wanted in some cases. If you don't want this behavior, you can use a python :obj:`list` instead of the :class:`nlp.Sequence`.

- a :class:`nlp.ClassLabel` feature specifies a field with a predefined set of classes which can have labels associated to them and will be stored as integers in the dataset. This field will be stored and retrieved as an integer value and two conversion methodes, :func:`nlp.ClassLabel.str2int` and :func:`nlp.ClassLabel.int2str` can be used to convert from the label names to the associate integer value and vice-versa.

- a :class:`nlp.Value` feature specifies a single typed value, e.g. ``int64`` or ``string``. The types supported are all the `non-nested types of Apache Arrow <https://arrow.apache.org/docs/python/api/datatypes.html#factory-functions>`__ among which the most commonly used ones are ``int64``, ``float32`` and ``string``.
- :class:`nlp.Tensor` is mostly supported to have a compatibility layer with the TensorFlow Datasets library and can host a 0D or 1D array. A 0D array is equivalent to a :class:`nlp.Value` of the same dtype while a 1D array is equivalent to a :class:`nlp.Sequence` of the same dtype and fixed length.
- eventually, two features are specific to Machine Translation: :class:`nlp.Translation` and :class:`nlp.TranslationVariableLanguages`. We refere to the package reference for more details on these features.

