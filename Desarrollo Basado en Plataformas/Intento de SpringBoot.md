```java
package com.example.calculator;  
  
import org.springframework.http.HttpStatus;  
import org.springframework.http.ResponseEntity;  
import org.springframework.web.bind.annotation.*;  
  
@RestController  
public class CalculatorController {  
  
    private final CalculatorService calculatorService;  
  
    public CalculatorController(CalculatorService calculatorService) {  
        this.calculatorService = calculatorService;  
    }  
    @GetMapping("/suma/{a}/{b}")  
    public double suma(@PathVariable double a, @PathVariable double b) {  
        return calculatorService.sumar(a, b);  
    }  
    @GetMapping("/resta/{a}/{b}")  
    public double resta(@PathVariable double a, @PathVariable double b) {  
        return calculatorService.restar(a, b);  
    }  
    @GetMapping("/multiplicacion/{a}/{b}")  
    public double multiplicacion(@PathVariable double a, @PathVariable double b) {  
        return calculatorService.multiplicar(a, b);  
    }  
    @GetMapping("/division/{a}/{b}")  
    public ResponseEntity<?> division(@PathVariable double a, @PathVariable double b) {  
        try {  
            double result = calculatorService.dividir(a, b);  
            return ResponseEntity.ok(result);  
        } catch (ArithmeticException divisionException) {  
            return ResponseEntity.status(HttpStatus.UNPROCESSABLE_ENTITY).body("Error aritmetico: " + divisionException.getMessage());  
        }    }    }
```
