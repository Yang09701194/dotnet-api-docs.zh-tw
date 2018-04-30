<span data-ttu-id="fd68f-101">在下列狀況下，搭配使用以字元為主的索引與 <xref:System.Text.StringBuilder.Chars%2A> 屬性可能極為緩慢：</span><span class="sxs-lookup"><span data-stu-id="fd68f-101">Using character-based indexing with the <xref:System.Text.StringBuilder.Chars%2A> property can be extremely slow under the following conditions:</span></span>

- <span data-ttu-id="fd68f-102"><xref:System.Text.StringBuilder> 執行個體很大 (例如，它包含幾萬個字元)。</span><span class="sxs-lookup"><span data-stu-id="fd68f-102">The <xref:System.Text.StringBuilder> instance is large (for example, it consists of several tens of thousands of characters).</span></span>
- <span data-ttu-id="fd68f-103"><xref:System.Text.StringBuilder> 是「塊狀」。</span><span class="sxs-lookup"><span data-stu-id="fd68f-103">The <xref:System.Text.StringBuilder> is "chunky."</span></span> <span data-ttu-id="fd68f-104">也就是說，重複呼叫方法 (例如 <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType>) 已自動展開物件的 <xref:System.Text.StringBuilder.Capacity%2A?displayProperty=nameWithType> 屬性並配置記憶體的新區塊給它。</span><span class="sxs-lookup"><span data-stu-id="fd68f-104">That is, repeated calls to methods such as <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> have automatically expanded the object's <xref:System.Text.StringBuilder.Capacity%2A?displayProperty=nameWithType> property and allocated new chunks of memory to it.</span></span>

<span data-ttu-id="fd68f-105">由於每個字元的存取會行經整個連結的區塊清單來尋找要編入索引的正確緩衝區，因此會嚴重影響效能。</span><span class="sxs-lookup"><span data-stu-id="fd68f-105">Performance is severely impacted because each character access walks the entire linked list of chunks to find the correct buffer to index into.</span></span>

> [!NOTE]
>  <span data-ttu-id="fd68f-106">即使對於大型「塊狀」<xref:System.Text.StringBuilder> 物件，使用 <xref:System.Text.StringBuilder.Chars%2A> 對一個或少數字元進行以索引為主的存取，也只有些許的效能影響；一般來說，這是 **0(n)** 作業。</span><span class="sxs-lookup"><span data-stu-id="fd68f-106">Even for a large "chunky" <xref:System.Text.StringBuilder> object, using the <xref:System.Text.StringBuilder.Chars%2A> property for index-based access to one or a small number of characters has a negligible performance impact; typically, it is an **0(n)** operation.</span></span> <span data-ttu-id="fd68f-107">逐一查看 <xref:System.Text.StringBuilder> 物件中的字元時，就會發生顯著的效能影響，這是 **O(n^2)** 作業。</span><span class="sxs-lookup"><span data-stu-id="fd68f-107">The significant performance impact occurs when iterating the characters in the <xref:System.Text.StringBuilder> object, which is an **O(n^2)** operation.</span></span> 

<span data-ttu-id="fd68f-108">如果在 <xref:System.Text.StringBuilder> 物件中使用以字元為主的索引時遇到效能問題，您可以使用下列任一因應措施：</span><span class="sxs-lookup"><span data-stu-id="fd68f-108">If you encounter performance issues when using character-based indexing with <xref:System.Text.StringBuilder> objects, you can use any of the following workarounds:</span></span>

- <span data-ttu-id="fd68f-109">藉由呼叫 <xref:System.Text.StringBuilder.ToString%2A> 方法將 <xref:System.Text.StringBuilder> 執行個體轉換為 <xref:System.String>，然後存取字串中的字元。</span><span class="sxs-lookup"><span data-stu-id="fd68f-109">Convert the <xref:System.Text.StringBuilder> instance to a <xref:System.String> by calling the <xref:System.Text.StringBuilder.ToString%2A> method, then access the characters in the string.</span></span>

- <span data-ttu-id="fd68f-110">將現有 <xref:System.Text.StringBuilder> 物件的內容複製到預留大小的新 <xref:System.Text.StringBuilder> 物件。</span><span class="sxs-lookup"><span data-stu-id="fd68f-110">Copy the contents of the existing <xref:System.Text.StringBuilder> object to a new pre-sized <xref:System.Text.StringBuilder> object.</span></span> <span data-ttu-id="fd68f-111">因為新的 <xref:System.Text.StringBuilder> 物件不是塊狀，所以會改善效能。</span><span class="sxs-lookup"><span data-stu-id="fd68f-111">Performance improves because the new <xref:System.Text.StringBuilder> object is not chunky.</span></span> <span data-ttu-id="fd68f-112">例如: </span><span class="sxs-lookup"><span data-stu-id="fd68f-112">For example:</span></span>

   ```csharp
   // sbOriginal is the existing StringBuilder object
   var sbNew = new StringBuilder(sbOriginal.ToString(), sbOriginal.Length);
   ```
   ```vb
   ' sbOriginal is the existing StringBuilder object
   Dim sbNew = New StringBuilder(sbOriginal.ToString(), sbOriginal.Length)
   ```
- <span data-ttu-id="fd68f-113">藉由呼叫 <xref:System.Text.StringBuilder.%23ctor(System.Int32)> 建構函式，將 <xref:System.Text.StringBuilder> 物件的初始容量設定為大約等於其預期大小上限的值。</span><span class="sxs-lookup"><span data-stu-id="fd68f-113">Set the initial capacity of the <xref:System.Text.StringBuilder> object to a value that is approximately equal to its maximum expected size by calling the <xref:System.Text.StringBuilder.%23ctor(System.Int32)> constructor.</span></span> <span data-ttu-id="fd68f-114">請注意，即使 <xref:System.Text.StringBuilder> 很少達到其最大容量，這也會配置整個記憶體區塊。</span><span class="sxs-lookup"><span data-stu-id="fd68f-114">Note that this allocates the entire block of memory even if the <xref:System.Text.StringBuilder> rarely reaches its maximum capacity.</span></span>