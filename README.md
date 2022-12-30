<p align = "center">МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ
РОССИЙСКОЙ ФЕДЕРАЦИИ
ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ
ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ
«САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</p>
<br>
<p align = "center">Институт естественных наук и техносферной безопасности</p>
<p align = "center">Кафедра информатики</p>
<p align = "center">Пашаян Самвел Алексанович</p>
<br>
<p align = "center">Лабораторная работа №9</p>
<p align = "center">01.03.02 Прикладная математика и информатика</p>
<br>
<p align = "right" >Научный руководитель</p>
<p align = "right" >Соболев Евгений Игоревич</p>
<p align = "center" >Южно-Сахалинск</p>
<p align = "center" >2022 г.</p>
<p align = "center" ><b>ВВЕДЕНИЕ</b></p>
<p> <b> PHP  </b> (рекурсивный акроним словосочетания PHP: Hypertext Preprocessor) - это распространённый язык программирования общего назначения с открытым исходным кодом.</p>
<p> Вместо рутинного вывода HTML-кода командами языка (как это происходит, например, в Perl или C), скрипт PHP содержит HTML с встроенным кодом (в нашем случае, это вывод текста "Привет, я - скрипт PHP!"). Код PHP отделяется специальными начальным и конечным тегами <?php и ?>, которые позволяют "переключаться" в "PHP-режим" и выходить из него.
Код PHP отделяется специальными начальным и конечным тегами <?php и ?>, которые позволяют "переключаться" в "PHP-режим" и выходить из него.</p>
<p align = "center" > РЕШЕНИЕ ЗАДАЧ (ОСНОВНАЯ ЧАСТЬ) </p>

## Решение:
<!DOCTYPE html>
<HTML lang="ru">
<HEAD>
  <meta http-equiv="Content-Type: text/plain" content="text/html;charset=ISO-8859-1">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title> Лабораторная №9 </title>
</HEAD>

<BODY>
  <!-- Zad1 -->
  Zad1 
  <?php
  $today = date_create();
  $nextYear = date_format($today, "Y") + 1;
  $nyDate = date_create("$nextYear-01-01");
  $dateDiff = date_diff($today, $nyDate);
  echo "Осталось дней до НГ: $dateDiff->days";
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad2 -->
  Zad2 
  <form action="" method="POST">
    <label>Введите Год:</label>
    <input type="text" name="task2">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task2"])) {
    $year = $_POST["task2"];
    echo "Выбранный год $year - ", date("L", strtotime("$year-01-01")) ? "Високосный" : "Невисокосный";
  }
  ?>
  <!--------------->
  <br><br>

  <!-- Zad3 -->
  Zad3 
  <form action="" method="post">
    <label>Выберите дату:</label>
    <input type="date" name="task3">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task3"])) {
    $days = ["понедельник", "вторник", "среда", "четверг", "пятница", "суббота", "воскресенье"];
    $date = strtotime($_POST["task3"]);
    $day = date("N", $date);
    echo $days[$day - 1];
  }
  ?>
  <!--------------->
  <br><br>

  <!-- Zad4 -->
  Zad4
  <?php
  echo "Сегодня - ",date("jS \of F Y\, l");
  ?>
  <!--------------->
  <br><br>

  <!-- Zad5 -->
  Zad5
  <form action="" method="post">
    <label>Ваш день рождения: </label>
    <input type="date" name="task5">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task5"])) {
    $date = strtotime($_POST["task5"]);
    $day = date("d", $date);
    $month = date("m", $date);
    $year = date("Y") + 1;
    echo "Осталось дней до дня рождения: " . date_diff(date_create(), date_create("$day-$month-$year"))->days;
  }
  ?>
  <!--------------->
  <br><br>

  <!-- Zad6 -->
  Zad6
  <?php
  $today = date_create();
  $date = date_create("last Sunday of February");
  if ($today > $date) $date = date_create("last Sunday of February next year");
  echo "Осталось дней до Масленицы: " . date_diff($today, $date)->days;
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad7 -->
  Zad7
  <form action="" method="post">
    <label>Дата рождения (формат ДД.ММ):</label>
    <input type="text" name="task7">
    <input type="submit" value="Выполнить">
  </form>
  <?php
    function getZodiac($month, $day){
      $zodiacName = array(
          "Козерог", "Водолей", "Рыбы", 
          "Овен", "Телец", "Близнецы", 
          "Рак", "Лев", "Девы", 
          "Весы", "Скорпион", "Стрелец"
      );

      $zodiacDate = array(
          21, 20, 20, 20, 20, 20, 
          21, 22, 23, 23, 23, 23
      );

      if ($day < $zodiacDate[$month - 1]){
          $result = $zodiacName[$month - 1];
      }else{
          if($month == 12) $month = 0; 
          $result = $zodiacName[$month];
      }
      return $result;
    }

  if (isset($_POST["task7"])) {
    $str = $_POST["task7"];
    $date = explode(".", $str);
    if(count($date) > 1) {
      $zodiacSign = getZodiac($date[1], $date[0]);
      echo "Ваш знак зодиака: " . $zodiacSign, ","," было бы классно с вами дружить :)";
    }
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad8 -->
  Zad8
  <?php
  // Заполняем массив.
  $christmas = date("01-07");
  $hallowen = date("10-31");
  $edinstvo = date("11-04");
  $newYear = date("12-31");
  $holidays = [
    $christmas => "Рождество Христово",
    $hallowen => "Хэллоуин",
	$edinstvo => "День Народого Единства",
	$newYear => "Новый Год",
  ];
  // Вывод.
  $today = date("m-d");
  foreach ($holidays as $key => $value) {
    if ($today == $key) {
      $output = "С праздником: $value, дорогой пользователь!";
      break;
    }
    $output = "К сожалению, сегодня нет никакого праздника :(";
  }
  echo $output;
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad9 -->
  Zad9
  <?php
  function GetHoroscopeFor($zodiacSign)
  {
    switch($zodiacSign){
        case 'Овен':
          return 'Проявите любознательность и не упустите свой шанс добиться успеха. Новости, которые вы узнаете сегодня, позволят вам принять неожиданное решение и достичь того, что раньше сделать было непросто и не получалось.'; 
          break;
        case 'Телец':
          return 'Не оставайтесь в тени – больше общайтесь с окружающими и постарайтесь довести до конца то, что запланировали.'; 
          break;
        case 'Близнецы':
          return 'Остерегайтесь скандалов – сегодня вас могут обвинить в том, чего вы не делали. Не торопитесь с выводами – вероятно, что причина лежит не на поверхности и с ней предстоит вам еще разобраться.'; 
          break;
        case 'Рак':
          return 'Остерегайтесь ошибок, особенно в первой половине дня – они могут заставить вас долго с ними возиться. Не принимайте решений и постарайтесь заняться рутинной работой. '; 
          break;
        case 'Лев':
          return 'Остерегайтесь конфликтов и ссор, особенно в первой половине дня – в это время вам непросто будет контролировать свои эмоции и чувства.'; 
          break;
        case 'Девы':
          return 'Остерегайтесь сплетен и постарайтесь не вмешиваться в чужие дела. Сегодня вам очень захочется командовать окружающими и проявить инициативу, однако это будет не всегда разумно и может обострить отношения с окружающими. Держите эмоции при себе – это поможет избежать ненужных ссор и разочарований.'; 
          break;
        case 'Весы':
          return 'Оставайтесь при своем мнении – сегодня оно позволит вам избежать недоразумений и ошибок. Звезды советуют вам проявить силу характера – сегодня она поможет вам преодолеть как мелкие, так и крупные неприятности.'; 
          break;
        case 'Скорпион':
         return 'Сегодня вероятны не только задержки в делах, но и изменения в поведении и настрое окружающих вас людей. Не рассчитывайте на помощь со стороны или на то, что все получится с первого раза.'; 
          break;
        case 'Стрелец':
          return 'Остерегайтесь скандалов – в первой половине дня вы рискуете сами испортить отношения, даже самые лучшие. День хорош для отдыха, развлечений или рутинной, не творческой работы – именно она поможет вам немного остыть и подкорректировать свои планы.'; 
          break;
        case 'Козерог':
          return 'Не меняйте планы на будущее без веской причины. Сегодня вы будете недостаточно активны, поэтому будете чувствовать себя не в своей тарелке, особенно если окружающие будут вмешиваться в ваши дела и задумки.'; 
          break;
        case 'Водолей':
          return 'Спокойный и размеренный день, когда не стоит торопиться. Проявите доброжелательность и постарайтесь уделить больше внимания близким людям – за это они вам будут благодарны и помогут наладить отношения с теми, кто вам дорог.'; 
          break;
        case 'Рыбы':
          return 'Не меняйте планы на будущее – сегодня самое время реализовать то, что вы давно хотели сделать. Проявите доброжелательность и постарайтесь довести начатое до конца, несмотря ни на какие препятствия. '; 
          break;
    }
  }

  if (isset($_POST["task7"])) {
    $str = $_POST["task7"];
    $date = explode(".", $str);
    if(count($date) > 1) {
      $zodiacSign = getZodiac($date[1], $date[0]);
      echo "Так как вы: $zodiacSign.<br> Вот ваш гороскоп на сегодня:<br>" . GetHoroscopeFor($zodiacSign);
    }
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad10 -->
  Zad10
  <form action="" method="post">
    <textarea name="task10"></textarea>
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task10"])) {
    $text = $_POST["task10"];
    $alphabet = "АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯабвгдеёжзийклмнопрстуфхцчшщъыьэюя";
    echo "Количество слов в тексте: " . str_word_count($text, 0, $alphabet) . "<br>";
    echo "Количество символов в тексте: " . iconv_strlen($text) . "<br>";
    echo "Количество символов в тексте, за вычетом пробелов: " . (iconv_strlen($text) - substr_count($text, " ")) . "<br>";
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad11 -->
  Zad11
  <form action="" method="post">
    <textarea name="task11"></textarea>
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task11"])) {
    $text = $_POST["task11"];
    $len = mb_strlen($text);
    $chars_count = array_count_values(mb_str_split($text));
    foreach ($chars_count as $char => $count) {
      echo "% Символов: $char - " . round($count / $len * 100, 0, PHP_ROUND_HALF_EVEN) . "%<br>";
    }
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad12 -->
  Zad12
  <form action="" method="post">
    <label>Введите набор букв: (Пример: авкт) </label>
    <input type="text" name="task12">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task12"])) {
    $letters = mb_str_split($_POST["task12"]);
    $words = ["папа", "мама", "брат", "сестра", "бабушка", "дедушка", "студент", "абитуриент", "авто", "аниме", "фильм", "сериал", "утро", "день", "вечер", "ночь", "завтрак", "обед", "ужин", "сегодня", "завтра", "весело", "скучно", "хорошо", "да", "нет", "один", "два", "три"];
    $result = [];
    foreach ($words as $word) {
      $inString = true;
      foreach ($letters as $letter) {
        if (mb_stripos($word, $letter) === false) {
          $inString = false;
          break;
        }
      }
      if ($inString) array_push($result, $word);
    }

    echo "Слова, которые содержат все введенные буквы:<br>";
    for ($i = count($result) - 1; $i >= 0; $i--) {
      echo $result[$i];
      if ($i > 0) echo ", ";
    }
  }
  ?>
<!--------------->
<br><br>
  
  <!-- Zad13 -->
  Zad13
  <form action="" method="post">
  <label> Введите слова (на этот раз раздельно) </label>
    <textarea name="task13"></textarea>
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task13"])) {
    $words = explode(" ", $_POST["task13"]);
    sort($words);
    $prev = "";
    foreach ($words as $word) {
      $char = mb_str_split($word)[0];
      if ($prev !== $char)
        echo "<br>Слова на букву " . $char . ": ";
      else
        echo ", ";
      echo $word;
      $prev = $char;
    }
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad14 -->
  Zad14
  <form action="" method="post">
    <label>Строка на русском:</label>
    <input type="text" name="task14">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  function RusToLat($source = false)
  {
      if ($source) {
          $rus = [
              "А", "Б", "В", "Г", "Д", "Е", "Ё", "Ж", "З", "И", "Й", "К", "Л", "М", "Н", "О", "П", "Р", "С", "Т", "У", "Ф", "Х", "Ц", "Ч", "Ш", "Щ", "Ъ", "Ы", "Ь", "Э", "Ю", "Я",
              "а", "б", "в", "г", "д", "е", "ё", "ж", "з", "и", "й", "к", "л", "м", "н", "о", "п", "р", "с", "т", "у", "ф", "х", "ц", "ч", "ш", "щ", "ъ", "ы", "ь", "э", "ю", "я"
          ];
          $lat = [
              "A", "B", "V", "G", "D", "E", "Yo", "Zh", "Z", "I", "J", "K", "L", "M", "N", "O", "P", "R", "S", "T", "U", "F", "H", "C", "Ch", "Sh", "Shh", "\`\`", "Y`", "`", "E`", "Yu", "Ya", "a", "b", "v", "g", "d", "e", "yo", "zh", "z", "i", "j", "k", "l", "m", "n", "o", "p", "r", "s", "t", "u", "f", "h", "c", "ch", "sh", "shh", "``", "y`", "`", "e`", "yu", "ya"
          ];
          return str_replace($rus, $lat, $source);
      }
  }

  if (isset($_POST["task14"])) {
    echo "Line in English: " . RusToLat($_POST["task14"]);
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad15 -->
  Zad15
  <form action="" method="get">
    <input type="text" name="task15">
    <input type="submit" value="Выполнить"><br>
    <input type="radio" name="radio15" value="To" checked><label>В транслит</label>
    <input type="radio" name="radio15" value="From"><label>Из транслита</label>
  </form>
  <?php
  function LatToRus($source = false)
  {
      if ($source) {
          $rus = [
              "А", "Б", "В", "Г", "Д", "Е", "Ё", "Ж", "З", "И", "Й", "К", "Л", "М", "Н", "О", "П", "Р", "С", "Т", "У", "Ф", "Х", "Ц", "Ч", "Ш", "Щ", "Ъ", "Ы", "Ь", "Э", "Ю", "Я",
              "а", "б", "в", "г", "д", "е", "ё", "ж", "з", "и", "й", "к", "л", "м", "н", "о", "п", "р", "с", "т", "у", "ф", "х", "ц", "ч", "ш", "щ", "ъ", "ы", "ь", "э", "ю", "я"
          ];
          $lat = [
              "A", "B", "V", "G", "D", "E", "Yo", "Zh", "Z", "I", "J", "K", "L", "M", "N", "O", "P", "R", "S", "T", "U", "F", "H", "C", "Ch", "Sh", "Shh", "\`\`", "Y`", "`", "E`", "Yu", "Ya", "a", "b", "v", "g", "d", "e", "yo", "zh", "z", "i", "j", "k", "l", "m", "n", "o", "p", "r", "s", "t", "u", "f", "h", "c", "ch", "sh", "shh", "``", "y`", "`", "e`", "yu", "ya"
          ];
          return str_replace($lat, $rus, $source);
      }
  }

  if (isset($_POST["task15"])) {
    if ($_POST["radio15"] === "To")
      echo "Транслит: " . RusToLat($_POST["task15"]);
    else
      echo "Из транслита: " . LatToRus($_POST["task15"]);
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad16 -->
  Zad16
  <style>
    .correct {
      background-color: limegreen;
    }

    .wrong {
      background-color: red;
    }
  </style>
  <p><b>Ответы "да" или "нет":</b></p>
  <form action="" method="post">
    <?php
    $quests = [
      "Вопрос 1" => "да",
      "Вопрос 2" => "да",
      "Вопрос 3" => "нет",
      "Вопрос 4" => "да",
      "Вопрос 5" => "нет",
    ];

    $i = 0;
    foreach ($quests as $quest => $answer) {
      echo $quest . "<br>";
      if (isset($_POST["q$i"])) {
        echo "<p>Ваш ответ: " . $_POST["q$i"] . " - ";
        if ($_POST["q$i"] === $answer)
          echo '<span class = "correct">Ответ верный!';
        else
          echo '<span class = "wrong">Ответ неверный!';
        echo "</span></p>";
      } else
        echo '<input type="text" name="q' . $i . '"><br>';

      $i++;
    }
    ?>
    <input type="submit" value="Выполнить">
  </form>
  <!--------------->
  <br><br>
  
  <!-- Zad17 -->
  Zad17
  <form action="" method="post">
    <?php
    $quests = [
      "Вопрос 1" => "да",
      "Вопрос 2" => "нет",
      "Вопрос 3" => "нет",
      "Вопрос 4" => "да",
      "Вопрос 5" => "нет",
    ];

    $i = 0;
    foreach ($quests as $quest => $answer) {
      echo $quest . "<br>";
      if (isset($_POST["radio17$i"])) {
        echo "<p>Ваш ответ: " . $_POST["radio17$i"] . " - ";
        if ($_POST["radio17$i"] === $answer)
          echo '<span class = "correct">Ответ верный!';
        else
          echo '<span class = "wrong">Ответ неверный!';
        echo "</span></p>";
      } else
        echo '
        <input type="radio" name="radio17' . $i . '" value="да">
        <label>да</label>
        <input type="radio" name="radio17' . $i . '" value="нет">
        <label>нет</label>
        <br>
        ';

      $i++;
    }
    ?>
    <input type="submit" value="Выполнить">
  </form>
  <!--------------->
  <br><br>
  
  <!-- Zad18 -->
  Zad18
  <form action="" method="post">
    <?php
    $quests = [
      "Вопрос 1" => ["да", "нет"],
      "Вопрос 2" => ["да", "не знаю"],
      "Вопрос 3" => ["нет"],
      "Вопрос 4" => ["да"],
      "Вопрос 5" => ["нет", "не знаю"],
    ];

    $variants = [
      ["да", "нет", "не знаю"],
      ["да", "нет", "не знаю"],
      ["да", "нет", "не знаю"],
      ["да", "нет", "не знаю"],
      ["да", "нет", "не знаю"],
    ];

    $i = 0;
    foreach ($quests as $quest => $answer) {
      // Вопрос №
      echo $quest . "<br>";
      // Ваш ответ: 
      if (isset($_POST["submit"])) {
        echo "Ваш ответ: [";
        $userAnswer = [];
        for ($j = 0; $j < count($variants[$i]); $j++) {
          if (isset($_POST["radio18$i$j"])) {
            array_push($userAnswer, $_POST["radio18$i$j"]);
          }
        }
        // Ответ
        echo implode(", ", $userAnswer) . "] - ";
        // Верно/Неверно
        if (!array_diff($userAnswer, $answer) && !array_diff($answer, $userAnswer))
          echo '<span class = "correct">Ответ верный!';
        else
          echo '<span class = "wrong">Ответ неверный!';
        echo "</span></p>";
      } else {
        // Чекбоксы  
        for ($j = 0; $j < count($variants[$i]); $j++)
          echo '
            <input type="checkbox" name="radio18' . $i . $j . '" value="' . $variants[$i][$j] . '">
            <label>' . $variants[$i][$j] . '</label>
          ';
        echo "<br>";
      }
      $i++;
    }

    if (isset($_POST["reset"])) $_POST["submit"] = "";
    ?>
    <input type="submit" name="submit" value="Выполнить">
    <input type="submit" name="reset" value="Сбросить">
  </form>
  <!--------------->
  <br><br>
  
  <!-- Zad19 -->
  Zad19
  <form action="" method="post">
    <input type="text" name="task19">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task19"])) {
    $num = $_POST["task19"];
    $res = 1;
    for ($i = 1; $i <= $num; $i++) {
      $res *= $i;
    }
    echo "Ответ: " . $res;
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad20 -->
  Zad20
  <form action="" method="post">
    <label>a = </label>
    <input type="text" name="task20a">
    <label>b = </label>
    <input type="text" name="task20b">
    <label>c = </label>
    <input type="text" name="task20c">
    <br>
    <input type="submit" name="task20sbm" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task20sbm"])) {
    $a = $_POST["task20a"];
    $b = $_POST["task20b"];
    $c = $_POST["task20c"];
    $D = $b * $b - 4 * $a * $c;
    $d = sqrt(abs($D));

    echo "Ответ: ";
    if ($D == 0) {
      echo "x = " . (-$b + $d) / 2 / $a;
    } else if ($D > 0) {
      echo "x1 = " . (-$b + $d) / 2 / $a . ", ";
      echo "x2 = " . (-$b - $d) / 2 / $a;
    } else {
      echo "x1/2 = (" . -$b . htmlspecialchars_decode("&plusmn", ENT_QUOTES) . $d . "i) / " . 2 * $a;
    }
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad21 -->
  Zad21
  <form action="" method="post">
    <label>a = </label>
    <input type="text" name="task21a">
    <label>b = </label>
    <input type="text" name="task21b">
    <label>c = </label>
    <input type="text" name="task21c">
    <br>
    <input type="submit" name="task21sbm" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task21sbm"])) {
    $a = $_POST["task21a"];
    $b = $_POST["task21b"];
    $c = $_POST["task21c"];
    $sum = 0;
    $max;
    if ($a > $b) {
      $sum += $b * $b;
      $max = $a;
    } else {
      $sum += $a * $a;
      $max = $b;
    }
    if ($max > $c) {
      $sum += $c * $c;
      $max *= $max;
    } else {
      $sum += $max * $max;
      $max = $c * $c;
    }

    if ($max == $sum) echo "Тройка Пифагора";
    else echo "Не тройка Пифагора";
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad22 -->
  Zad22
  <form action="" method="post">
    <input type="text" name="task22">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task22"])) {
    $num = $_POST["task22"];
    $results = [];
    for ($i = 1; $i <= intdiv($num, 2); $i++) {
      if ($num % $i == 0)
        array_push($results, $i);
    }

    echo "Делители: " . implode(", ", $results);
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad23 -->
  Zad23
  <form action="" method="post">
    <input type="text" name="task23">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task23"])) {
    $num = $_POST["task23"];
    $results = [];
    $i = 1;
    while ($num != 1) {
      $i++;
      if ($num % $i == 0) {
        $num /= $i;
        array_push($results, $i);
        $i = 1;
      }
    }

    echo "Простые множители: " . implode(", ", $results);
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad24 -->
  Zad24
  <form action="" method="post">
    <input type="text" name="task24a">
    <input type="text" name="task24b">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task24a"]) && isset($_POST["task24b"])) {
    $a = $_POST["task24a"];
    $b = $_POST["task24b"];
    $results = [];
    for ($i = 1; $i <= intdiv(max($a, $b), 2); $i++) {
      if ($a % $i == 0 && $b % $i == 0)
        array_push($results, $i);
    }

    echo "Общие делители: " . implode(", ", $results);
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad25 -->
  Zad25
  <form action="" method="post">
    <input type="text" name="task25a">
    <input type="text" name="task25b">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task25a"]) && isset($_POST["task25b"])) {
    $a = $_POST["task25a"];
    $b = $_POST["task25b"];
    echo "НОД = " . gcd($a, $b);
  }

  function gcd($a, $b)
  {
    $a = abs($a);
    $b = abs($b);
    while ($b) {
      $temp = $b;
      $b = $a % $b;
      $a = $temp;
    }
    return $a;
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad26 -->
  Zad26
  <form action="" method="post">
    <input type="text" name="task26a">
    <input type="text" name="task26b">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task26a"]) && isset($_POST["task26b"])) {
    $a = $_POST["task26a"];
    $b = $_POST["task26b"];
    echo "НОК = " . lcm($a, $b);
  }

  function lcm($a, $b)
  {
    return abs($a * $b / gcd($a, $b));
  }
  ?>
  <!--------------->
  <br><br>
  
  <!-- Zad27 -->
  Zad27
  <form action="" method="post">
    <input type="text" name="task27a">
    <input type="text" name="task27b">
    <input type="text" name="task27c">
    <input type="submit" value="Выполнить">
  </form>
  <?php
  if (isset($_POST["task27a"]) && isset($_POST["task27b"]) && isset($_POST["task27c"])) {
    $d = $_POST["task27a"];
    $m = $_POST["task27b"];
    $y = $_POST["task27c"];
    $days = ["понедельник", "вторник", "среда", "четверг", "пятница", "суббота", "воскресенье"];

    echo "$d-$m-$y - " . $days[date("N", strtotime("$d.$m.$y")) - 1];
  }
  ?>
  <!--------------->
</BODY>
</HTML>
- - -
<p align = "center" > ВЫВОД </p>
<p> Итогом работы стало создание странички с использованием языка PHP. В ходе выполнения задания, мною были решены все выдвинутые задачи, сформулированные исходя из цели лабораторной работы, и в которых нужно было написать функции, выполняющие то или иное действие. Я поработал с различными переменными, выполняющими простейшие операции, где-то нужно было переделать код, а где-то прописать вручную полностью. Это позволяет сделать вывод, что цель данной лабораторной работы успешно достигнута. </p>
