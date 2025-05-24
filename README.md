# SI_2025_lab2_213282
## Viktor Bozhinovski 213282

## Цикломатска комплексност
33 - 26 + 2 = 9


## слика од граф
![CFD drawio2213282](https://github.com/user-attachments/assets/8b0edb48-42ce-4612-abda-710916ca3cc1)


## Тест случаи според критериумот Every statement
 
@Test
public void testAllItemsNull() {
    RuntimeException ex = assertThrows(RuntimeException.class, () -> {
        SILab2.checkCart(null, "1234567890123456");
    });
    assertEquals("allItems list can't be null!", ex.getMessage());
}

@Test
public void testValidItemNoDiscountNo30() {
    List<Item> items = List.of(new Item("Apple", 1, 100, 0));
    double result = SILab2.checkCart(items, "1234567890123456");
    assertEquals(100.0, result);
}

@Test
public void testItemWithDiscountAnd30() {
    List<Item> items = List.of(new Item("TV", 1, 350, 0.1));
    double result = SILab2.checkCart(items, "1234567890123456");
    assertEquals(285.0, result); // -30 + (350*0.9*1) = -30 + 315 = 285
} 

## Тест случаи според критериумот Every path

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.util.List;
import java.util.Arrays;
public class SILab2Test {

@Test
    public void testAllItemsNull() {
        RuntimeException ex = assertThrows(RuntimeException.class, () -> {
            SILab2.checkCart(null, "1234567890123456");
        });
        assertEquals("allItems list can't be null!", ex.getMessage());
    }

 @Test
    public void testItemWithoutDiscount() {
        List<Item> items = List.of(new Item("item1", 1, 100, 0.0));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(100.0, result);
    }


   @Test
    public void testItemWithDiscountAndPriceOver300() {
        List<Item> items = List.of(new Item("item2", 5, 350, 0.1));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(1545.0, result);
    }

    
  @Test
    public void testMultipleCondition1() {
        List<Item> items = List.of(new Item("item", 1, 100, 0.0));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(100.0, result);
    }

   @Test
    public void testMultipleCondition2() {
        List<Item> items = List.of(new Item("item", 11, 100, 0.0));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(1070.0, result);
    }

   @Test
    public void testMultipleCondition3() {
        List<Item> items = List.of(new Item("item", 1, 100, 0.1));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(60.0, result);
    }

   @Test
    public void testMultipleCondition4() {
        List<Item> items = List.of(new Item("item", 12, 100, 0.2));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(930.0, result);
    }

   @Test
    public void testMultipleCondition5() {
        List<Item> items = List.of(new Item("item", 1, 301, 0.0));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(271.0, result);
    }

   @Test
    public void testMultipleCondition6() {
        List<Item> items = List.of(new Item("item", 11, 301, 0.0));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(3271.0, result);
    }

   @Test
    public void testMultipleCondition7() {
        List<Item> items = List.of(new Item("item", 2, 350, 0.2));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(530.0, result); 
    }

   @Test
    public void testMultipleCondition8() {
        List<Item> items = List.of(new Item("item", 12, 400, 0.3));
        double result = SILab2.checkCart(items, "1234567890123456");
        assertEquals(3330.0, result);
    }
}

## Објаснување на напишаните unit tests
## testAllItemsNull	Го проверува случајот кога allItems == null. Се очекува да фрли исклучок – се покрива првата if наредба.
## testItemWithoutDiscount	Еден валиден артикл без попуст. Ги покрива пресметките кога условот за -30 не е исполнет и нема попуст.
## testItemWithDiscountAndPriceOver300	Артикл кој го исполнува условот price > 300, па се одзема 30. Има и попуст, па се пресметува со попуст. Се покриваат повеќе гранки од кодот.
