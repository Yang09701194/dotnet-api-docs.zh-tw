### <a name="crash-in-selector-when-removing-an-item-from-a-custom-incc-collection"></a><span data-ttu-id="d1ca4-101">從自訂 INCC 集合中移除項目時，選取器發生損毀</span><span class="sxs-lookup"><span data-stu-id="d1ca4-101">Crash in Selector when removing an item from a custom INCC collection</span></span>

|   |   |
|---|---|
|<span data-ttu-id="d1ca4-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d1ca4-102">Details</span></span>|<span data-ttu-id="d1ca4-103">在下列狀況中可能發生 <code>T:System.InvalidOperationException</code>：</span><span class="sxs-lookup"><span data-stu-id="d1ca4-103">An <code>T:System.InvalidOperationException</code> can occur in the following scenario:</span></span><ul><li><span data-ttu-id="d1ca4-104"><code>T:System.Windows.Controls.Primitives.Selector</code> 的 ItemsSource 是具有 <code>T:System.Collections.Specialized.INotifyCollectionChanged</code> 自訂實作的集合。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-104">The ItemsSource for a <code>T:System.Windows.Controls.Primitives.Selector</code> is a collection with a custom implementation of <code>T:System.Collections.Specialized.INotifyCollectionChanged</code>.</span></span></li><li><span data-ttu-id="d1ca4-105">已從集合中移除選取的項目。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-105">The selected item is removed from the collection.</span></span></li><li><span data-ttu-id="d1ca4-106"><code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code> 具有 <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> = -1 (表示未知的位置)。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-106">The <code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code> has <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> = -1 (indicating an unknown position).</span></span></li></ul><span data-ttu-id="d1ca4-107">例外狀況的呼叫堆疊的開頭：at System.Windows.Threading.Dispatcher.VerifyAccess() at System.Windows.DependencyObject.GetValue(DependencyProperty dp) at System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject element)。如果應用程式有一個以上的發送器執行緒，在 .Net 4.5 中可能會發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-107">The exception's callstack begins at System.Windows.Threading.Dispatcher.VerifyAccess() at System.Windows.DependencyObject.GetValue(DependencyProperty dp) at System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject element)This exception can occur in .Net 4.5 if the application has more than one Dispatcher thread.</span></span> <span data-ttu-id="d1ca4-108">在 .Net 4.7 中，具有單一發送器執行緒的應用程式也可能會發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-108">In .Net 4.7 the exception can also occur in applications with a single Dispatcher thread.</span></span> <span data-ttu-id="d1ca4-109">此問題已在 .Net 4.7.1 中修正。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-109">The issue is fixed in .Net 4.7.1.</span></span>|
|<span data-ttu-id="d1ca4-110">建議</span><span class="sxs-lookup"><span data-stu-id="d1ca4-110">Suggestion</span></span>|<span data-ttu-id="d1ca4-111">升級至 .Net 4.7.1。</span><span class="sxs-lookup"><span data-stu-id="d1ca4-111">Upgrade to .Net 4.7.1.</span></span>|
|<span data-ttu-id="d1ca4-112">範圍</span><span class="sxs-lookup"><span data-stu-id="d1ca4-112">Scope</span></span>|<span data-ttu-id="d1ca4-113">次要</span><span class="sxs-lookup"><span data-stu-id="d1ca4-113">Minor</span></span>|
|<span data-ttu-id="d1ca4-114">版本</span><span class="sxs-lookup"><span data-stu-id="d1ca4-114">Version</span></span>|<span data-ttu-id="d1ca4-115">4.7</span><span class="sxs-lookup"><span data-stu-id="d1ca4-115">4.7</span></span>|
|<span data-ttu-id="d1ca4-116">類型</span><span class="sxs-lookup"><span data-stu-id="d1ca4-116">Type</span></span>|<span data-ttu-id="d1ca4-117">執行階段</span><span class="sxs-lookup"><span data-stu-id="d1ca4-117">Runtime</span></span>|
