# AGENTS.md - import-converter

## Zweck & Verantwortung

Das `import-converter` Modul bietet ein **generisches Converter-Framework** für Daten-Transformationen im Pacemaker Import-System. Es ist ein **Tier 4 Modul** und dient als Basis für spezialisierte Converter.

**Hauptverantwortung:**
- Generisches Converter-Framework
- Dezimal-Konvertierung und Daten-Transformationen
- Observer Pattern für Converter-Hooks
- Basis für spezialisierte Converter (Product, Customer, etc.)

## Architektur & Design Patterns

### Kern-Klassen
- **ConverterInterface**: Basis-Interface für Converter
- **DecimalConverter**: Spezialisiert für Dezimal-Konvertierung
- **AbstractConverter**: Basis-Klasse für Converter
- **ConverterObserver**: Observer für Converter-Hooks

### Verwendete Patterns
- **Observer Pattern**: Für Converter-Hooks
- **Strategy Pattern**: Verschiedene Konvertierungs-Strategien
- **Factory Pattern**: Für Converter-Erstellung

## Abhängigkeiten

### Externe Pakete
- **Keine** - Nur Framework-Implementierungen

### TechDivision Dependencies
- **import** ^18.0.0 - Core Framework

### Abhängig von diesem Modul (5 Reverse Dependencies)
1. **import-converter-customer-attribute** - Customer Attribute Converter
2. **import-converter-ee** - EE Converter
3. **import-converter-product-attribute** - Product Attribute Converter
4. **import-converter-product-category** - Product Category Converter
5. **import-cli-simple** - Master CLI

## Wichtige Entry Points

### Converter Klassen
```php
// Converter Interface
ConverterInterface::convert($value): mixed
ConverterInterface::getSubject(): SubjectInterface

// Decimal Converter
DecimalConverter::convert($value): float
DecimalConverter::setPrecision($precision): void

// Converter Observer
ConverterObserver::handle($row): void
```

### Verwendungsbeispiel
```php
// In Importern
$converter = new DecimalConverter();
$price = $converter->convert('19.99');

// In Observers
class CustomConverter extends AbstractConverter {
    public function convert($value) {
        return strtoupper($value);
    }
}
```

## Events & Extension Points

**Keine Events** - Tier 4 Framework-Modul

## Hints für KI-Agenten

### Wichtig zu verstehen
1. **Tier 4 Modul**: Basis für spezialisierte Converter
2. **Generisches Framework**: Für verschiedene Konvertierungs-Strategien
3. **Observer Pattern**: Für Converter-Hooks
4. **5 Dependents**: Basis für spezialisierte Converter

### Bei Änderungen
- **Framework-Kompatibilität**: Beachte alle 5 Dependents
- **Observer-Kompatibilität**: Neue Observers sollten optional sein
- **Backward Compatibility**: Alte Converter sollten noch funktionieren

## Bekannte Einschränkungen

- **Generisches Framework**: Keine spezialisierte Logik
- **Keine Validierung**: Validierung erfolgt in Importern
- **Keine Error Handling**: Error Handling erfolgt in Importern

## Zusammenfassung

`import-converter` ist ein **Tier 4 Modul**, das ein generisches Converter-Framework für Daten-Transformationen bietet. Es ist die Basis für spezialisierte Converter und unterstützt verschiedene Konvertierungs-Strategien.

**Für Agenten:** Verstehe dieses Modul als **Converter-Framework** mit Observer Pattern.
