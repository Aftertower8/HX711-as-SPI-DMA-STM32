# HX711-as-SPI-DMA
Projekt rekrutacyjny KNR Rover Team do sekcji embedded - Odczyt danych z ADC HX711 z wykorzystaniem DMA

# Opis:
Waga z dokładnością 0,1g, pomiary do 1000g. Działa przez UART, tarowanie pod klawiszem 't'.
Napisane na Nucleo-F103RB z wykorzystaniem HX711 i belki tensometrycznej 1000g.
Zamiast bit-bangingu wykorzystuje moduł DMA - mniejsze obciązenie procesora, możliwość wykonywania innych operacji w trakcie pomiaru.


# Źródła:
- https://github.com/ufnalski/hx711_non_blocking_spi_g431kb - użycie MOSI jako CLK
- HX711 Datasheet
