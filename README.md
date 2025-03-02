![CleanShot 2025-03-02 at 14.54.23](https://hackmd.io/_uploads/ry4nxKZsJx.png)


### 依賴項目 (Dependencies)  
- `accompanist-systemuicontroller`：用於修改狀態列顏色。  
- `material-icons-extended`：提供更多可用的圖示。  

### 設定狀態列顏色 (Set Status Bar Color)  
- 建立 `setBarColor` 可組合函式 (Composable)。  
- 使用 `rememberSystemUiController()` 取得 `SystemUiController`。  
- 透過 `SideEffect` 設定 `setSystemBarsColor()`，使狀態列顏色與背景一致。  
- 在主題 (`AppTheme`) 中呼叫 `setBarColor(MaterialTheme.colorScheme.background)`。

### 建立 Home 畫面 (Home Screen)  
- 定義 `HomeScreen` 可組合函式，並加上 `@Preview` 以便預覽。  
- 使用 `Scaffold` 作為主要佈局容器。  
- `Scaffold` 內部包含 Bottom Bar (稍後定義)。  
- 定義四個區塊：`WalletSection`、`CardSection`、`FinanceSection`、`CurrenciesSection`。  
- 各區塊間使用 `Spacer(modifier = Modifier.height(16.dp))` 來增加間距。  
- 所有內容包在 `Column` 內，並使用 `Modifier.fillMaxSize().padding(paddingValues)`。

### 建立 Bottom Navigation Bar  
- 建立 `BottomNavigationBar` 可組合函式。  
- 建立 `BottomNavigationItem` 的資料類別 (Data Class)，包含 `title` (標題) 和 `icon` (圖示)。  
- 定義四個 `BottomNavigationItem`：Home、Wallet、Notifications、Account。  
- 使用 `NavigationBar` 作為底部導航容器，並包含 `Row`。  
- `Row` 使用 `Modifier.background(MaterialTheme.colorScheme.inverseOnSurface)` 來設置底色。  
- 迴圈建立 `NavigationBarItem`，其中第一個預設為選取狀態 (`selected = index == 0`)。  
- `icon` 屬性設定為 `ImageVector`，並應用 `tint = MaterialTheme.colorScheme.onBackground`。  
- `label` 為對應的 `title`，顏色與 `icon` 一致。  

### 建立 Wallet 區塊 (Wallet Section)  
- 建立 `WalletSection` 可組合函式，並加上 `@Preview` 以便預覽。  
- 使用 `Row` 作為主要佈局容器，`horizontalArrangement = Arrangement.SpaceBetween` 使內容兩端對齊。  
- `Column` 內包含 `Text("Wallet")` 及餘額顯示 (`Text("34,000")`)，字體大小為 `24.sp` 並設為粗體。  
- 右側為 `Icon`，外層包裹 `Box`，並使用 `Modifier.clip(RoundedCornerShape(15.dp))` 設定圓角。  
- `Box` 設定 `backgroundColor = MaterialTheme.colorScheme.secondaryContainer`，且具備 `clickable` 效果。  
- `Icon` 設定 `imageVector = Icons.Rounded.Search`，顏色為 `MaterialTheme.colorScheme.onSecondaryContainer`。

### 設計卡片資料結構
- 創建 `Card` 類別，包含以下屬性：`cardType` (String)、`cardNumber` (String)、`cardName` (String)、`balance` (Double)、`color` (Brush)。
- 使用 `Brush` 來設定卡片的漸層顏色。

### 定義卡片資料
- 以 `cards` 列表來儲存多個卡片，包含不同卡片類型 (如 Visa、MasterCard)。
- 每張卡片具有隨機的卡號、卡片名稱、餘額以及顏色。

### 建立漸層顏色函數
- 創建 `getGradient` 函數來返回漸層顏色，接受起始與結束顏色並回傳 `Brush`。

### 使用 LazyRow 顯示卡片
- 在 `CardsSection` 中使用 `LazyRow` 顯示卡片資料，並根據 `cards.size` 動態加載卡片。
- 根據卡片的索引來設定最後一張卡片的結尾邊距，避免第一張卡片的左邊距失衡。

### 顯示卡片項目
- 創建 `CardItem` 函數來顯示每一張卡片。
- 設定每張卡片的圖片，根據 `cardType` 判斷顯示 Visa 或 MasterCard 圖片。
- 使用 `Box` 包含卡片的所有元素，並設定圓角邊框、背景顏色、大小及點擊效果。

### 內容排版
- 使用 `Column` 排版卡片內部的元素，包含卡片圖片、卡片名稱、餘額和卡號。
- 設定每個文本的樣式，包括字體大小、顏色和字重。

### 測試與調整
- 在主畫面進行預覽，確保卡片顯示正常且可滑動。
- 調整最後一張卡片的邊距，確保所有卡片間距均勻。

### 創建 `Finance` 資料類別
- 定義 `Finance` 類別，包含 `icon`、`name` 和 `background` 屬性。

### 定義四個 `Finance` 項目
- 創建四個 `Finance` 項目，分別為 `my business`、`my wallet`、`Finance analytics` 和 `my transactions`，並設置各自的背景顏色和圖示。

### 創建 `FinanceSection` 函數
- 使用 `Composable` 創建 `FinanceSection`，並加入 `Preview` 註解。
- 顯示標題 `Finance`，設置字體大小為 24sp，字體顏色為背景色，字體加粗，並添加 16dp 內邊距。

### 使用 `LazyRow` 顯示 `Finance` 項目
- 使用 `LazyRow` 顯示項目，並使用 `finance.size` 來迭代 `Finance` 項目。
- 設置 `lastPadding` 為 `16dp`，判斷是否為最後一項。

### 創建 `FinanceItem` 顯示單一項目
- 定義 `FinanceItem` 函數來顯示每個 `Finance` 項目。
- 設置圓角、背景顏色、尺寸等屬性，圖示顏色為白色，名稱字體設為加粗。

### 設定內部元素排版
- 在 `FinanceItem` 內部，使用 `Column` 來顯示圖示和名稱。
- 使用 `Box` 包裹圖示，並設置圓角背景、填充和尺寸。

### 添加間距與顯示效果
- 在 `FinanceItem` 的每個元素周圍添加適當的內邊距，讓項目顯示整齊。

### 創建貨幣資料類別
- 創建 `Currency` 資料類別，包含 `name` (String)、`buy` (Float)、`sale` (Float) 和 `icon` (ImageVector) 屬性。
- 在 `main` 包中創建包含貨幣資料的 `currencies` 列表。

### 定義貨幣資料
- 定義幾個貨幣資料項目，如 `USD`、`Euro` 和 `Yen`，並隨機指定買入賣出價格。
- 每個貨幣都有相應的圖示，例如 `USD` 使用 `icons.rounded.attack_money`。

### 設定顯示狀態
- 使用 `mutableStateOf` 和 `remember` 創建可變狀態來控制貨幣部分是否顯示。
- 創建 `iconState` 來改變箭頭圖示的方向，實現開關的動畫效果。

### 設定 Column 和 Row 結構
- 使用 `Column` 來布局外圍結構，並設置圓角和背景色。
- 使用 `Row` 來顯示圖示和文字，並設置對齊、間距和填充。

### 創建可點擊的圓形圖示
- 圓形圖示包裹在 `Box` 中，設置背景顏色並使其可點擊。
- 點擊時切換 `isVisible` 狀態，控制貨幣部分顯示與否。

### 顯示貨幣名稱和狀態
- 使用 `Text` 顯示 "Currencies" 文本，設置字體顏色、大小、粗細等屬性。
- 添加 `Spacer` 來控制圖示和文本之間的間距。

### 顯示分隔線
- 使用 `Spacer` 創建一條分隔線，並設置高度為 1dp，背景顏色為主題顏色。

### 根據可見狀態顯示貨幣項目
- 使用 `BoxWithConstraints` 計算容器寬度並將其分為三個區域，讓每個區域的內容對齊。
- 使用 `LazyColumn` 顯示貨幣項目，並根據 `isVisible` 狀態決定是否顯示。

### 使用 `LazyColumn` 顯示貨幣項目
- 在 `LazyColumn` 中根據 `currencies` 列表的大小創建貨幣項目。
- 為每個貨幣項目傳遞索引，顯示貨幣的買入、賣出價及名稱。

### 創建 `Currency Section` 的 Composable 函式
- 建立 `CurrencyItem` 函式，接受 `index` 和 `width` 兩個參數
- 使用 `DP` 型別的 `width` 來對齊文本
- 在該函式中創建 `currency`，並使用 `Row` 排列圖示和文本
- 利用 `modifier.fillMaxWidth()` 和 `padding` 來調整佈局

### 設計顯示貨幣圖示
- 使用 `Box` 包裹貨幣圖示，並設置圓角、背景顏色、內邊距
- 使用 `Icon` 顯示貨幣圖示，設置顏色為白色
- 圖示大小設為 `18.dp`

### 顯示並處理展開/收起的動畫
- 使用 `Box` 來包裹所有內容，並設置對齊方式為底部居中
- 添加適當的內邊距來確保展開和收起動畫的順暢性
- 使用 `Column` 和 `fillMaxSize` 保證內容的填充

### 顯示貨幣名稱與買賣價格
- 在 `Row` 中添加貨幣名稱、買價和賣價文本
- 設定文本大小，並為買賣價格添加美元符號
- 使用 `padding` 來調整文本間距

### 修正 UI 誤差與對齊
- 修正圖示和文本對齊問題，將圖示和文本放入 `Row` 中
- 調整 `modifier.width` 來避免顯示錯誤
- 調整 `padding` 和 `verticalAlignment`，確保元素正確對齊

### 處理額外的空間和佈局
- 移除不必要的內邊距，改用 `horizontalPadding` 來縮減不必要的空間
- 測試應用在不同主題下的顯示效果，確認各種顯示配置下的佈局正常運行

### 優化 UI 顯示
- 添加適當的 `Spacer` 或 `padding` 來改善視覺效果
- 測試應用在不同螢幕配置下的顯示效果，確保沒有問題


# Terminology
- **Composable**：Jetpack Compose 中的可組合函式，用於構建 UI 元件。  
- **Modifier**：Compose 的修飾符，用於設定 UI 元件的大小、間距、背景等屬性。  
- **Scaffold**：Compose 提供的佈局結構，包含頂部欄、底部導航欄、浮動按鈕等常見 UI 元件。  
- **NavigationBar**：Compose Material3 提供的底部導航欄元件，用於顯示多個選項。  
- **ImageVector**：Compose 中用於表示向量圖標的資料類型，適用於 Icon 元件。  
- **SystemUiController**：Accompanist 庫提供的工具，可用於控制系統 UI，如狀態列顏色。  
- **SideEffect**：Compose 的效應函式，適用於非組合範圍內的狀態變更。  
- **ColorScheme**：Material3 主題的顏色系統，包含背景色、主要顏色、次要顏色等。  
- **Dynamic Color**：Material3 支援的動態配色，根據系統主題或壁紙變更應用顏色。  
- **Preview**：Compose 的預覽註解，可在 IDE 內部即時查看 UI 組件的顯示效果。  
- **Padding**：用於設定元件與周圍元素的間距，通常搭配 `Dp` 使用。  
- **FillMaxSize**：Modifier 設定，使元件填滿可用空間。  
- **Arrangement.SpaceBetween**：Row 或 Column 內部的排列方式，確保元素之間平均分布間距。  
- **VerticalAlignment.CenterVertically**：Row 內元素的垂直對齊方式，確保居中對齊。  
- **Row**：Compose 中的佈局元件，允許子元件水平排列。  
- **Column**：Compose 中的佈局元件，允許子元件垂直排列。  
- **Box**：Compose 的容器元件，可用於重疊顯示元素或自訂背景。  
- **RoundedCornerShape**：用於設定圓角的形狀，可應用於 Box 或按鈕等元件。  
- **Spacer**：Compose 提供的間距元件，用於在佈局中增加固定高度或寬度的空間。  
- **FontWeight.Bold**：設定文字的字重為粗體。  
- **Text**：Compose 中的文字顯示元件。  
- **Dp**：Compose 用於設定距離與尺寸的單位，類似於 Android 傳統的 dp。  
- **OnBackground**：Material3 顏色系統中的文字顏色，適用於背景上的內容。  
- **SecondaryContainer**：Material3 色彩系統中的次要容器顏色，適用於次要內容的背景。  
- **Clickable**：Modifier 屬性，讓元件具有點擊效果。  
- **NavigationBarItem**：Compose Material3 提供的底部導航欄按鈕元件，可用於顯示圖示與標籤。  
- **Tint**：用於設定 Icon 或 Image 的顏色。  
- **MutableState**：Compose 的可變狀態變數，可觸發 UI 重新繪製。  
- **Remember**：Compose 的狀態儲存函式，確保 UI 內部狀態在重組時保持不變。  
- **LaunchedEffect**：Compose 提供的副作用函式，適用於異步操作。  
- **MaterialTheme**：Compose Material3 的主題提供者，包含顏色、排版與形狀設定。  
- **Theme**：Compose 內的主題設定，可應用於整個應用程式的 UI 風格。  
- **LocalContext**：Compose 內獲取當前 Context 物件的方法，適用於存取資源或啟動 Activity。  
- **MutableStateListOf**：Compose 中的可變列表狀態，可用於存儲並監聽列表變化。  
- **AnimationSpec**：Compose 動畫 API 的規格，可用於設定動畫曲線與時間。  
- **Crossfade**：Compose 提供的淡入淡出動畫效果，可用於切換 UI 元件。  
- **LazyColumn**：Compose 提供的高效能垂直列表，可動態載入內容。  
- **LazyRow**：Compose 提供的高效能水平列表，可動態載入內容。  
- **rememberSaveable**：與 `remember` 類似，但可在螢幕旋轉時保留狀態。  
- **AnimatedVisibility**：Compose 提供的可見性動畫效果，可用於顯示或隱藏 UI 元件。  
- **OutlinedButton**：Material3 的輪廓按鈕，與傳統按鈕不同，具有邊框但無填充色。  
- **FloatingActionButton (FAB)**：Compose 提供的浮動操作按鈕，常見於右下角。  
- **ScaffoldState**：Compose Scaffold 的狀態控制類型，適用於控制抽屜或 Snackbar。  
- **SnackbarHost**：Compose 提供的 Snackbar 容器，可顯示短暫的提示訊息。  
- **TopAppBar**：Material3 提供的頂部應用欄，可用於顯示標題與操作按鈕。  
- **OutlinedTextField**：Material3 提供的輸入框，具有邊框設計。  
- **KeyboardActions**：Compose 提供的鍵盤操作監聽，可處理輸入完成或點擊事件。  
- **TextFieldDefaults**：Compose 提供的預設樣式，可用於設定 TextField 的顏色與樣式。  
- **DropdownMenu**：Compose 提供的下拉選單元件，可用於顯示選擇列表。  
- **ExposedDropdownMenuBox**：Material3 提供的下拉式選單容器，支援展開與收合動畫。  
- **Divider**：Compose 提供的分隔線元件，可用於分割內容區塊。  
- **Canvas**：Compose 提供的自訂繪圖元件，可用於繪製圖形或動畫。  
- **PathEffect**：Compose 提供的路徑效果，可用於設定虛線或其他繪圖樣式。
- **Composable**: 在Jetpack Compose中，表示可以進行UI組件構建的函數，它能夠被動態更新並且是聲明式的。
- **LazyRow**: 一個橫向的滾動列表，只有當用戶需要滾動到某項時才會加載該項，從而提高性能。
- **Padding**: 控制元素邊界的空白區域，常用來設置UI元素與其他元素之間的間距。
- **Modifier**: 用來修飾或調整UI元素屬性的工具，在Jetpack Compose中用於設置元素的外觀或行為。
- **Painter**: 用於顯示圖片資源的工具，可以從資源中加載圖片並將其顯示在UI上。
- **Brush**: 一種顏色填充方式，常用來創建漸變色效果，可以在UI中提供多種顏色的過渡。
- **Card**: 在UI中用於顯示內容區塊的組件，通常包括圖片、文字和其他視覺元素。
- **Column**: 垂直排列的UI元素容器，每個子元素在上下方向上排列。
- **Box**: 一個可容納子元素的容器，允許更靈活的佈局設置。
- **Spacer**: 用於在UI中插入空白區域的元素，常用來調整布局中元素之間的距離。
- **Gradient**: 漸變色，顏色在兩個或更多顏色之間逐漸過渡，通常用來創建視覺上引人注目的背景。
- **State**: 在Jetpack Compose中，用來追蹤UI組件狀態的變量，可以觸發UI的重新組織。
- **Clickability**: 用於設置元素是否可被點擊的屬性，通常用於交互式UI元素。
- **Text**: 在UI中顯示文字的組件，可以設置字體、顏色、大小等屬性。
- **FontWeight**: 字體粗細的設置，通常有regular、bold、light等選項。
- **FontSize**: 字體的大小，單位通常為sp（scale-independent pixels）。
- **Modifier.clip**: 用來將元素裁剪為特定形狀的修飾符，常用於實現圓角或圓形的效果。
- **Shape**: 用來定義UI元素外觀形狀的屬性，常用於圓角、矩形等形狀。
- **LazyColumn**: 一種縱向的滾動列表，僅加載當前顯示的項目，對於長列表來說更有效。
- **StateHoisting**: 將狀態從Composable函數中提升到外部，以便在不同的組件之間共享狀態。
- **Scrollable**: 設置UI元素可滾動的屬性，常用於當內容超出屏幕顯示區域時。
- **HorizontalArrangement**: 用來設置水平排列元素的方式，例如左對齊、居中或右對齊。
- **VerticalArrangement**: 用來設置垂直排列元素的方式，例如上下對齊、間距或填充。
- **remember**: 用來記住某個狀態或數據，避免在UI重組時丟失，通常用於持久化小範圍的狀態。
- **onClick**: 用於設置按鈕或其他交互式元素的點擊事件處理函數。
- **CardType**: 在此上下文中指代不同種類的卡片（如Visa或MasterCard），用於確定顯示的圖片和信息。
- **DataClass**: 一種用於保存數據的Kotlin類型，常用於定義數據結構，並自動提供基本的函數如`equals`、`hashCode`等。
- **List**: 用來存儲一組數據的集合類型，在這裡存儲的是不同的卡片項目。
- **Int**: 代表整數類型，通常用來表示計數或索引等數值。
- **Long**: 用來表示長整數類型，常用於表示較大的數值，如銀行餘額等。
- **Double**: 用來表示雙精度浮點數類型，常用於表示包含小數的數值。
- **Brush.horizontalGradient**: 創建一個橫向的漸變色刷，用於背景顏色的過渡效果。
- **CardSection**: 一個專門顯示卡片項目的UI區塊，通常由多個卡片組成。
- **Items**: 用來表示數據源中的一組項目，通常配合`LazyRow`或`LazyColumn`使用以實現高效的UI渲染。
- **Index**: 在列表或集合中的位置，通常用來指示當前項目的索引。
- **ScrollableColumn**: 一個可以縱向滾動的列容器，用來顯示超出屏幕大小的內容。
- **OnClickListener**: 在UI中為元素設置點擊事件的處理器，用來處理用戶的交互。
- **Clickable**: 設置元素是否可以被點擊，與交互性相關。
- **CardItem**: 單個卡片項目，用來顯示卡片的詳細信息。
- **ContentDescription**: 用於為視覺元素提供描述文字，幫助屏幕閱讀器識別內容。
- **Brush.linearGradient**: 用來創建線性漸變的畫刷，常用於背景填充或其他視覺效果。
- **ShapeableImageView**: 用於顯示圖片的視圖，支持圓角或其他自定義形狀。
- **Composables**：在Jetpack Compose中用來建立UI元件的函數，可以無狀態地組合成複雜UI。
- **LazyRow**：Jetpack Compose的組件，提供懶加載的橫向滾動列表，只在需要時才會加載項目。
- **Modifier**：在Jetpack Compose中用來修飾UI元件的屬性，可以設定大小、顏色、背景等。
- **ImageVector**：用於儲存矢量圖形的類型，通常用於顯示SVG圖片或向量圖形。
- **Column**：Jetpack Compose中的一個排版容器，將子元件按垂直方向排列。
- **Text**：Jetpack Compose中的文本顯示元件，用於顯示字符串。
- **Padding**：用於設定UI元件內部邊距的屬性，確保元件不會與周圍元素緊貼。
- **Background**：用來設置元件背景的屬性，可以指定顏色、圖片或漸層色。
- **Clip**：用來剪裁UI元件形狀的屬性，通常配合圓角使用。
- **Tint**：設定圖像或圖標顏色的屬性，通常用來改變圖像或圖標的顏色。
- **FontWeight**：設定文字的粗細屬性，常見的選項有`bold`和`normal`。
- **FontSize**：用來設定字體大小的屬性，通常以SP為單位。
- **Spacer**：用於創建空白間隔的UI元件，可以在布局中插入間隔。
- **VerticalArrangement**：設定垂直排列方式的屬性，常用選項有`spaceBetween`、`center`等。
- **ClickListener**：用來處理元件點擊事件的處理函數。
- **Color**：Jetpack Compose中的顏色類型，用來設定UI元件的顏色。
- **Brush**：用於創建漸層或其他複雜背景效果的顏色類型。
- **LazyColumn**：類似於LazyRow，但用於垂直滾動的列表，提供懶加載功能。
- **Card**：常用的容器組件，用來顯示具有陰影和圓角的卡片式UI。
- **State**：在Jetpack Compose中用來存儲和管理UI狀態的類型。
- **Preview**：Jetpack Compose中的一個註解，幫助開發者快速查看UI元件的預覽效果。
- **Icon**：用於顯示圖標的UI元件，通常由向量圖形或圖片組成。
- **TextStyle**：用來定義文字樣式的類型，可以包含字體、顏色、大小等屬性。
- **MaterialTheme**：Jetpack Compose中提供的默認樣式，包含顏色、字型等設置。
- **Surface**：提供背景顏色、圓角、陰影等效果的容器組件。
- **Clickability**：用來設定UI元件是否可點擊的屬性，通常配合`Modifier`使用。
- **Scrollable**：設定元件是否可以滾動的屬性，通常用於長內容顯示。
- **PaddingValues**：用來指定每個方向的邊距（左、右、上、下）的數據類型。
- **onClick**：在Jetpack Compose中設置點擊事件的屬性，用來指定點擊時的操作。
- **Alignment**：用來設定UI元件在其容器中的對齊方式，常用的有`start`、`center`、`end`等。
- **Modifier.clipToBounds**：用來剪裁UI元件的邊界，使其在顯示時不超出其容器。
- **Context**：提供應用程序環境信息的類型，通常用來訪問資源、啟動活動等。
- **IconButton**：包含圖標的按鈕元件，通常用來實現簡單的點擊操作。
- **Coil**：Jetpack Compose中用來加載圖片的庫，支持圖片的異步加載。
- **ContentDescription**：用於描述UI元件的內容，通常對於無法顯示的元素（如圖像）很重要。
- **isClickable**：判斷UI元件是否可點擊的屬性，用於設置點擊效果。
- **Shape**：用來定義UI元件形狀的類型，常用的有圓角矩形、圓形等。
- **MaterialIcon**：Material Design中的圖標，通常以`Icon`組件形式呈現。
- **InteractionSource**：用來管理UI元件交互的源，如點擊、觸摸等。
- **Dp**：密度無關像素，用來設定元素大小或間距，以應對不同設備的顯示密度。
- **ClickEffect**：點擊效果，通常用來為元件添加點擊時的視覺反應。
- **SurfaceColor**：設定元件背景顏色的屬性，用於創建包含陰影和圓角的背景。
- **Gradients**：漸層顏色效果，用來創建顏色過渡的視覺效果。
- **Scaffold**：用來構建基本UI結構的容器，通常包括應用的導航、內容區域等。
- **Box**：Jetpack Compose中的容器元件，用來覆蓋或疊加其他UI元件。
- **ResId**：資源ID，指向應用程序資源（如圖片、字串、顏色等）的唯一標識符。
- **OnClickListener**：用來處理UI元件的點擊事件，設置對應的邏輯處理。
- **backgroundColor**：設定UI元件背景顏色的屬性。
- **ParentLayout**：UI元件的父容器，用來包含和控制子元件的排列。
- **FontFamily**：設置文字字體家族的屬性，用來定義顯示字體樣式。
- **IconResource**：用來引用圖標資源的ID，通常以`R.drawable`方式引用。
- **Composable**：在 Jetpack Compose 中，Composable 是一個標記函式，用來建立可重複使用的 UI 元件，並且可以響應狀態改變。
- **State**：狀態是用來保存 UI 中變化的數據，並且能夠觸發 UI 的更新。
- **MutableState**：可變狀態，允許對狀態進行更改，並觸發界面更新。
- **remember**：Jetpack Compose 中的一個函式，用來記住狀態或變量，讓其在組件重新組合時保持不變。
- **Icon**：一個圖標元件，通常用於顯示小型圖片，常用於 UI 中的按鈕或標誌。
- **ImageVector**：用來描述矢量圖像的類型，適用於在 Compose 中創建動態圖標或矢量圖形。
- **Modifier**：修飾符，用來配置 UI 元素的外觀、大小、佈局等屬性。
- **BoxWithConstraints**：在 Jetpack Compose 中，BoxWithConstraints 是一個布局容器，允許獲取並操作其可用的最大寬度或高度。
- **LazyColumn**：一種可滾動的列布局，支持懶加載，僅渲染顯示在屏幕上的項目，從而提高性能。
- **Column**：列布局元件，允許在垂直方向上排列一組 UI 元素。
- **Row**：行布局元件，用來在水平方向上排列一組 UI 元素。
- **Text**：用來顯示文字的組件，支持多種文本樣式和顏色設定。
- **Padding**：為組件添加內邊距，控制元素與其他元素之間的空間。
- **Spacer**：一個佔位符組件，用來在布局中創建空間或間距。
- **Size**：設置 UI 元素的尺寸，通常用於調整寬度或高度。
- **Background**：設置 UI 元素的背景顏色或圖片。
- **RoundedCornerShape**：用來創建圓角形狀的修飾符，用於視覺效果。
- **Clip**：將視圖裁剪成特定形狀，如圓形或矩形。
- **AnimateContentSize**：使組件在大小變更時具有動畫效果，實現平滑過渡。
- **FillMaxWidth**：設置元素的寬度填充其父容器的最大寬度。
- **TextAlign**：控制文本對齊方式，如左對齊、右對齊或居中對齊。
- **FontSize**：設置文本的字體大小。
- **FontWeight**：設置文本的字重（例如，正常、加粗）。
- **OnClickListener**：設置點擊事件的監聽器，用於觸發操作。
- **MaterialTheme**：Jetpack Compose 中的一種主題設置，控制應用的顏色、字體等樣式。
- **SecondaryColor**：主題中的次要顏色，通常用於次要的 UI 元素。
- **Surface**：一個 Material Design 元素，表示具有背景的視圖容器，通常用於卡片或對話框等元素。
- **Icons**：預設的圖標集，用於快速構建 UI 圖標。
- **ImageVector**：表示圖標的類型，能夠在 Compose 中顯示矢量圖形。
- **LazyColumn Items**：LazyColumn 中的每個項目，通常是懶加載顯示的數據項。
- **Grid**：網格布局，用來將內容分成多列和多行，通常用於顯示圖片或項目。
- **Constraints**：限制條件，用於控制元素在佈局中的尺寸和位置。
- **HorizontalAlignment**：水平方向上的對齊方式，控制元素在行內的分佈。
- **VerticalAlignment**：垂直方向上的對齊方式，控制元素在列中的分佈。
- **ModifierSize**：調整元素尺寸的修飾符，控制元素的寬度和高度。
- **MaxWidth**：設置元素的最大寬度，限制其不超過父容器的最大寬度。
- **ColumnScope**：在列布局中創建範圍，允許將元素放入列中。
- **RowScope**：在行布局中創建範圍，允許將元素放入行中。
- **Weight**：權重，用來設置元素在布局中的相對大小比例。
- **Stateful**：指擁有可變狀態的組件，狀態會隨著用戶操作或其他變化而更新。
- **EventHandler**：事件處理器，負責處理 UI 元素的事件，如點擊或滾動等。
- **Composable Function**：可組合函式，用於構建 UI 組件，在 Jetpack Compose 中是基本的 UI 元件單位。
- **LazyLoading**：懶加載技術，僅加載可見的項目，從而提高性能和內存使用效率。
- **Box**：一種容器元件，可以在其內部放置其他 UI 元素，並可對其進行定位。
- **ConstraintsModifier**：用來為元素設置約束條件，確定其在佈局中的位置和尺寸。
- **Composable**：Jetpack Compose 中用來創建 UI 組件的函數，表示可組合的 UI 元件。
- **Modifier**：用來修改 UI 元件屬性如大小、顏色、對齊等的物件。
- **DP (Density-independent Pixels)**：無論螢幕密度如何，保持一致大小的單位。
- **Box**：一種佈局元件，用來包含其他 UI 元件，可以設定其大小和對齊。
- **Row**：用來水平排列 UI 元件的佈局容器。
- **Column**：用來垂直排列 UI 元件的佈局容器。
- **Icon**：表示圖示的 UI 元件，通常用來顯示圖片或向用戶呈現某種動作。
- **Text**：顯示文本內容的 UI 元件。
- **Padding**：UI 元件的內部間距，用來設置元件與其內容的空間。
- **Alignment**：用來對齊元件的屬性，控制其在父容器中的位置。
- **Vertical Alignment**：垂直方向上的對齊方式，通常設置為中心、頂部或底部。
- **Clip**：用來剪裁視圖的邊界，通常與形狀結合使用。
- **Shape**：用來定義視圖形狀的屬性，如圓角矩形、圓形等。
- **Tint**：調整顏色或圖片的顏色，通常應用於圖示或圖片上。
- **Content Description**：給視覺元素提供描述，常用於無障礙性設計。
- **Weight**：文本或 UI 元件的粗細屬性，通常用於設置字體的粗細。
- **Text Size**：文字的大小，通常以 SP (Scale-independent Pixels) 作為單位。
- **FillMaxSize**：設置 UI 元件填滿其父容器的大小。
- **BoxWithConstraints**：在有約束的情況下佈局的容器，常用於獲取父容器的大小限制。
- **Horizontal Padding**：設定水平方向的間距，通常是元件左右的空間。
- **Spacer**：用來在 UI 元件之間添加空間的元素。
- **State**：在 Jetpack Compose 中，用來存儲和管理 UI 元件狀態的物件。
- **Lambda**：在 Kotlin 中，表示可傳遞的匿名函數，通常用於設置 UI 元件的回調或行為。
- **IconButton**：包含圖示的按鈕 UI 元件。
- **Scaffold**：一種用於構建應用 UI 基礎結構的容器，通常用於包含底部導航欄或頂部欄。
- **LazyColumn**：延遲加載的垂直列表元件，通常用於顯示大量的列表項目。
- **LazyRow**：延遲加載的水平列表元件，通常用於顯示大量的列表項目。
- **Coroutine**：Kotlin 中的輕量級線程，用來執行異步操作。
- **Click Modifier**：用來為元件添加點擊事件處理的修飾符。
- **Theme**：設定應用的整體樣式，包括顏色、字型、形狀等。
- **Surface**：Jetpack Compose 中的基礎 UI 元件，通常用來作為其他元件的背景。
- **Border**：為元件設置邊框的屬性。
- **Gradient**：漸變顏色，常用於背景設計中，提供多種顏色過渡效果。
- **ScrollState**：用來管理滾動視圖的狀態，通常與可滾動元件一起使用。
- **Snackbar**：顯示短暫信息的 UI 元件，通常用於顯示成功、錯誤或提示消息。
- **Surface Modifier**：用來設置 Surface 元件外觀的修飾符，通常包含背景、形狀、陰影等。
- **Visibility**：設置元件是否顯示的屬性，通常用於隱藏或顯示 UI 元件。
- **Interaction Source**：用來處理 UI 元件交互行為的源，通常與點擊或觸摸事件有關。
- **Clickable Modifier**：使 UI 元件可被點擊的修飾符。
- **FontFamily**：設置文本的字體族，通常包括多種字型樣式。
- **FontWeight**：設置字體的粗細屬性。
- **ImageVector**：描述矢量圖像的物件，通常用於創建可縮放的圖示。
- **Accompanist**：Jetpack Compose 的輔助庫，用於提供額外功能，如圖片加載、動態樣式等。
- **Popup**：顯示浮動界面的 UI 元件，通常用於顯示選單或提示框。
- **Transition**：用於創建動畫效果的機制，能夠在不同狀態間過渡。
- **Dialog**：對話框元件，用來顯示模態對話框。
