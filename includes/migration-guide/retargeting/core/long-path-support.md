### <a name="long-path-support"></a><span data-ttu-id="904b1-101">長路徑支援</span><span class="sxs-lookup"><span data-stu-id="904b1-101">Long path support</span></span>

|   |   |
|---|---|
|<span data-ttu-id="904b1-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="904b1-102">Details</span></span>|<span data-ttu-id="904b1-103">從以 .NET Framework 4.6.2 為目標的應用程式開始，支援長路徑 (最多 32K 個字元)，且已移除對於路徑長度的 260 個字元 (或 <code>MAX_PATH</code>) 限制。若為重新編譯以 .NET Framework 4.6.2 為目標的應用程式，先前因為路徑超過 260 個字元而擲回 <xref:System.IO.PathTooLongException?displayProperty=name> 的程式碼路徑，現在將只有在下列情況下擲回 <xref:System.IO.PathTooLongException?displayProperty=name>：</span><span class="sxs-lookup"><span data-stu-id="904b1-103">Starting with apps that target the .NET Framework 4.6.2, long paths (of up to 32K characters) are supported, and the 260-character (or <code>MAX_PATH</code>) limitation on path lengths has been removed.For apps that are recompiled to target the .NET Framework 4.6.2, code paths that previously threw a <xref:System.IO.PathTooLongException?displayProperty=name> because a path exceeded 260 characters will now throw a <xref:System.IO.PathTooLongException?displayProperty=name> only under the following conditions:</span></span><ul><li><span data-ttu-id="904b1-104">路徑的長度大於 <xref:System.Int16.MaxValue> (32,767) 個字元。</span><span class="sxs-lookup"><span data-stu-id="904b1-104">The length of the path is greater than <xref:System.Int16.MaxValue> (32,767) characters.</span></span></li><li><span data-ttu-id="904b1-105">作業系統傳回 <code>COR_E_PATHTOOLONG</code> 或其對應項。</span><span class="sxs-lookup"><span data-stu-id="904b1-105">The operating system returns <code>COR_E_PATHTOOLONG</code> or its equivalent.</span></span></li></ul><span data-ttu-id="904b1-106">若為以 .NET Framework 4.6.1 和更早版本為目標的應用程式，每當路徑超過 260 個字元時，執行階段就會自動擲回 <xref:System.IO.PathTooLongException?displayProperty=name>。</span><span class="sxs-lookup"><span data-stu-id="904b1-106">For apps that target the .NET Framework 4.6.1 and earlier versions, the runtime automatically throws a <xref:System.IO.PathTooLongException?displayProperty=name> whenever a path exceeds 260 characters.</span></span>|
|<span data-ttu-id="904b1-107">建議</span><span class="sxs-lookup"><span data-stu-id="904b1-107">Suggestion</span></span>|<span data-ttu-id="904b1-108">若為以 .NET Framework 4.6.2 為目標的應用程式，如果不需要長路徑支援，您可以透過將下列內容新增至 <code>app.config</code> 檔案的 <code>&lt;runtime&gt;</code> 區段以選擇退出長路徑支援︰</span><span class="sxs-lookup"><span data-stu-id="904b1-108">For apps that target the .NET Framework 4.6.2, you can opt out of long path support if it is not desirable by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre><span data-ttu-id="904b1-109">若為以舊版 .NET Framework 為目標但卻在 .NET Framework 4.6.2 或更新版本上執行的應用程式，則可將下列內容新增至 <code>app.config</code> 檔案的 <code>&lt;runtime&gt;</code> 區段，以選擇加入長路徑支援：</span><span class="sxs-lookup"><span data-stu-id="904b1-109">For apps that target earlier versions of the .NET Framework but run on the .NET Framework 4.6.2 or later, you can opt in to long path support by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="904b1-110">範圍</span><span class="sxs-lookup"><span data-stu-id="904b1-110">Scope</span></span>|<span data-ttu-id="904b1-111">次要</span><span class="sxs-lookup"><span data-stu-id="904b1-111">Minor</span></span>|
|<span data-ttu-id="904b1-112">版本</span><span class="sxs-lookup"><span data-stu-id="904b1-112">Version</span></span>|<span data-ttu-id="904b1-113">4.6.2</span><span class="sxs-lookup"><span data-stu-id="904b1-113">4.6.2</span></span>|
|<span data-ttu-id="904b1-114">類型</span><span class="sxs-lookup"><span data-stu-id="904b1-114">Type</span></span>|<span data-ttu-id="904b1-115">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="904b1-115">Retargeting</span></span>|
