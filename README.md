# Luxembourg vat number format validators config

![Code Coverage Badge](./badge.svg)

This package provides a preconfigured configuration class for vat number format validators for Luxembourg country.
Is an extension of the package https://github.com/rocketfellows/specific-country-vat-number-format-validators-config.

## Installation

```shell
composer require rocketfellows/lu-vat-number-format-validators-config
```

## Dependencies

- https://github.com/rocketfellows/specific-country-vat-number-format-validators-config v1.0.0;
- https://github.com/rocketfellows/lu-vat-format-validator v1.0.0;

## References

- https://github.com/rocketfellows/country-vat-format-validator-interface
- https://github.com/arslanim/iso-standard-3166

## List of package components

- **_rocketfellows\LUVatNumberFormatValidatorsConfig\LUVatNumberFormatValidatorsConfig_** - preconfigured configuration class for vat number format validators for Luxembourg country;

## LUVatNumberFormatValidatorsConfig description

A configuration class that provides a match for the vat number format validators for the country Luxembourg.

Class interface:
- **_getCountry_** - returns Luxembourg **_Country_** instance;
- **_getValidators_** - returns validators tuple

When initializing the default configuration, the **_getValidators_** function returns a tuple with a single validator - an instance of LUVatFormatValidator.

```php
$config = new LUVatNumberFormatValidatorsConfig();

$config->getCountry();      // returns Luxembourg Country instance
$config->getValidators();   // returns CountryVatFormatValidators with one item - instance of LUVatFormatValidator
```

You can override the default validator by initializing the configuration class object with a new default validator through the first parameter of the class constructor.
Attention - validator must implement interface **_CountryVatFormatValidatorInterface_**.

```php
$newDefaultValidator = new NewDefaultValidator();                       // instance of CountryVatFormatValidatorInterface
$config = new LUVatNumberFormatValidatorsConfig($newDefaultValidator);  // initialize with new default validator

$config->getValidators();   // returns CountryVatFormatValidators with one item - $newDefaultValidator
```

You can add additional validators to the default validator via the second constructor parameter.

Attention - additional validators parameter must be instance of tuple **_CountryVatFormatValidators_**.
And each additional validator must implement interface **_CountryVatFormatValidatorInterface_**.

```php
$firstAdditionalValidator = new FirstAdditionalValidator();   // instance of CountryVatFormatValidatorInterface
$secondAdditionalValidator = new SecondAdditionalValidator(); // instance of CountryVatFormatValidatorInterface

$config = new LUVatNumberFormatValidatorsConfig(
    null,
    (
        new CountryVatFormatValidators(
            $firstAdditionalValidator,
            $secondAdditionalValidator
        )
    )
);

// returns CountryVatFormatValidators with three items:
// default preconfigured validator by default - instance of LUVatFormatValidator
// $firstAdditionalValidator - from additional tuple
// $secondAdditionalValidator - from additional tuple
$config->getValidators();
```

You can also completely rebuild the configuration by passing the default validator and a tuple of additional validators to the config class constructor.

```php
$defaultValidator = new DefaultValidator();                   // instance of CountryVatFormatValidatorInterface
$firstAdditionalValidator = new FirstAdditionalValidator();   // instance of CountryVatFormatValidatorInterface
$secondAdditionalValidator = new SecondAdditionalValidator(); // instance of CountryVatFormatValidatorInterface

$config = new LUVatNumberFormatValidatorsConfig(
    $defaultValidator,
    (
        new CountryVatFormatValidators(
            $firstAdditionalValidator,
            $secondAdditionalValidator
        )
    )
);

// returns CountryVatFormatValidators with three items:
// $defaultValidator from constructor first parameter
// $firstAdditionalValidator - from additional tuple
// $secondAdditionalValidator - from additional tuple
$config->getValidators();
```

More use case examples can be found in the package's unit tests.

## Contributing

Welcome to pull requests. If there is a major changes, first please open an issue for discussion.

Please make sure to update tests as appropriate.
