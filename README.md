{\rtf1\ansi\ansicpg936\cocoartf2821
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 WidgetMetadata = \{\
  id: "jable",\
  title: "Jable",\
  description: "\uc0\u33719 \u21462 Jable\u28909 \u38376 \u24433 \u29255 \u27036 \u21333 ",\
  author: "nibiru",\
  site: "https://github.com/quantumultxx/FW-Widgets",\
  version: "1.0.1",\
  requiredVersion: "0.0.1",\
  modules: [\
    \{\
      title: "\uc0\u28909 \u38376 \u24433 \u29255 ",\
      description: "\uc0\u28909 \u38376 \u24433 \u29255 ",\
      requiresWebView: false,\
      functionName: "loadPage",\
      params: [\
        \{\
          name: "url",\
          title: "\uc0\u21015 \u34920 \u22320 \u22336 ",\
          type: "constant",\
          description: "\uc0\u21015 \u34920 \u22320 \u22336 ",\
          value:\
            "https://jable.tv/hot/?mode=async&function=get_block&block_id=list_videos_common_videos_list",\
        \},\
        \{\
          name: "sort_by",\
          title: "\uc0\u25490 \u24207 ",\
          type: "enumeration",\
          description: "\uc0\u25490 \u24207 ",\
          enumOptions: [\
            \{\
              title: "\uc0\u25152 \u26377 \u26102 \u38388 ",\
              value: "video_viewed",\
            \},\
            \{\
              title: "\uc0\u26412 \u26376 \u28909 \u38376 ",\
              value: "video_viewed_month",\
            \},\
            \{\
              title: "\uc0\u26412 \u21608 \u28909 \u38376 ",\
              value: "video_viewed_week",\
            \},\
            \{\
              title: "\uc0\u20170 \u26085 \u28909 \u38376 ",\
              value: "video_viewed_today",\
            \},\
          ],\
        \},\
        \{\
          name: "from",\
          title: "\uc0\u39029 \u30721 ",\
          type: "page",\
          description: "\uc0\u39029 \u30721 ",\
          value: "1",\
        \},\
      ],\
    \},\
    \{\
      title: "\uc0\u20013 \u25991 \u23383 \u24149 ",\
      description: "\uc0\u20013 \u25991 \u23383 \u24149 \u24433 \u29255 ",\
      requiresWebView: false,\
      functionName: "loadPage",\
      params: [\
        \{\
          name: "url",\
          title: "\uc0\u21015 \u34920 \u22320 \u22336 ",\
          type: "constant",\
          description: "\uc0\u21015 \u34920 \u22320 \u22336 ",\
          value:\
            "https://jable.tv/categories/chinese-subtitle/?mode=async&function=get_block&block_id=list_videos_common_videos_list",\
        \},\
        \{\
          name: "sort_by",\
          title: "\uc0\u25490 \u24207 ",\
          type: "enumeration",\
          description: "\uc0\u25490 \u24207 ",\
          enumOptions: [\
            \{\
              title: "\uc0\u26368 \u26032 \u21457 \u24067 ",\
              value: "post_date",\
            \},\
            \{\
              title: "\uc0\u26368 \u22810 \u35266 \u30475 ",\
              value: "video_viewed",\
            \},\
            \{\
              title: "\uc0\u26368 \u22810 \u25910 \u34255 ",\
              value: "most_favourited",\
            \},\
          ],\
        \},\
        \{\
          name: "from",\
          title: "\uc0\u39029 \u30721 ",\
          type: "page",\
          description: "\uc0\u39029 \u30721 ",\
          value: "1",\
        \},\
      ],\
    \},\
  ],\
\};\
\
async function loadPage(params = \{\}) \{\
  const sections = await loadPageSections(params);\
  const items = sections.flatMap((section) => section.items);\
  return items;\
\}\
\
async function loadPageSections(params = \{\}) \{\
  try \{\
    let url = params.url;\
    if (!url) \{\
      throw new Error("\uc0\u22320 \u22336 \u19981 \u33021 \u20026 \u31354 ");\
    \}\
    if (params["sort_by"]) \{\
      url += `&sort_by=$\{params.sort_by\}`;\
    \}\
    if (params["from"]) \{\
      url += `&from=$\{params.from\}`;\
    \}\
    // 1. \uc0\u33719 \u21462 HTML\u20869 \u23481 \
    console.log("=== \uc0\u33719 \u21462 HTML\u20869 \u23481  ===");\
    const response = await Widget.http.get(url, \{\
      headers: \{\
        "User-Agent":\
          "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36",\
        Accept:\
          "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",\
      \},\
    \});\
\
    if (!response || !response.data || typeof response.data !== "string") \{\
      throw new Error("\uc0\u26080 \u27861 \u33719 \u21462 \u26377 \u25928 \u30340 HTML\u20869 \u23481 ");\
    \}\
\
    const htmlContent = response.data;\
    console.log(`\uc0\u33719 \u21462 \u21040 HTML\u20869 \u23481 \u38271 \u24230 : $\{htmlContent.length\} \u23383 \u31526 `);\
\
    // 2. \uc0\u35299 \u26512 HTML\
    console.log("\\n=== \uc0\u35299 \u26512 HTML ===");\
    const $ = Widget.html.load(htmlContent);\
    const sectionSelector = ".site-content .py-3,.pb-e-lg-40";\
    const itemSelector = ".video-img-box";\
    const coverSelector = "img";\
    const durationSelector = ".absolute-bottom-right .label";\
    const titleSelector = ".title a";\
\
    let sections = [];\
    const sectionElements = $(sectionSelector).toArray();\
    \
    for (const sectionElement of sectionElements) \{\
      const $sectionElement = $(sectionElement);\
      const items = [];\
      const sectionTitle = $sectionElement.find(".title-box .h3-md").first().text().trim();\
      \
      const itemElements = $sectionElement.find(itemSelector).toArray();\
      for (const itemElement of itemElements) \{\
        const $itemElement = $(itemElement);\
        const titleId = $itemElement.find(titleSelector).first();\
        const url = titleId.attr("href") || "";\
        \
        if (url && url.includes("jable.tv")) \{\
          const durationId = $itemElement.find(durationSelector).first();\
          const coverId = $itemElement.find(coverSelector).first();\
          const cover = coverId.attr("data-src") || coverId.attr("src");\
          const video = coverId.attr("data-preview");\
          const title = titleId.text().trim();\
          const duration = durationId.text().trim();\
          \
          items.push(\{\
            id: url,\
            type: "video",\
            title: title,\
            durationText: duration,\
            posterPath: cover,\
            previewUrl: video,\
            link: url,\
            metadata: \{\
              posterShape: "landscape",\
              mediaType: "video",\
            \}\
          \});\
        \}\
      \}\
\
      if (items.length > 0) \{\
        sections.push(\{\
          id: sectionTitle || "default-section",\
          type: "section",\
          title: sectionTitle || "\uc0\u40664 \u35748 \u26631 \u39064 ",\
          items: items,\
          style: "grid",\
          metadata: \{\
            layoutType: "grid",\
          \}\
        \});\
      \}\
    \}\
    \
    return sections;\
  \} catch (error) \{\
    console.error("\uc0\u27979 \u35797 \u36807 \u31243 \u20986 \u38169 :", error.message);\
    throw error;\
  \}\
\}}