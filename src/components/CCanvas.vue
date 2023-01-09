<template>
  <div class="container">
    <div class="row">
      <form class="form-horizontal">
        <div class="form-group">
          <label class="control-label col-sm-1" for="wadoURL">URL</label>
          {{ props.imageUrl ? props.imageUrl : "nothing" }}
          <div class="col-sm-8">
            <q-select
              v-model="selectedTool"
              label="Select Tool"
              :options="tools"
            />
            <input
              class="form-control"
              type="text"
              id="wadoURL"
              placeholder="Enter URL"
              :value="
                props.imageUrl
                  ? props.imageUrl
                  : 'https://rawgit.com/cornerstonejs/cornerstoneWebImageLoader/master/examples/Renal_Cell_Carcinoma.jpg'
              "
            />
          </div>
          <div class="col-sm-3">
            <button
              class="form-control btn btn-primary"
              type="button"
              id="downloadAndView"
            >
              Download and View
            </button>
            <button
              class="form-control btn btn-primary"
              type="button"
              @click="exportAnnotations"
            >
              Export Annotations
            </button>
            <button
              class="form-control btn btn-primary"
              type="button"
              @click="importAnnotations"
            >
              Import Annotations
            </button>
            <button
              class="form-control btn btn-primary"
              type="button"
              @click="activateBrushTool"
            >
              Brush Tool
            </button>
          </div>
        </div>
      </form>
    </div>

    <div
      oncontextmenu="return false"
      class="ccanvas disable-selection noIbar"
      unselectable="on"
      onselectstart="return false;"
      onmousedown="return false;"
    >
      <div id="dicomImage" class="dicom-image"></div>
    </div>
  </div>
</template>

<script setup>
import Hammer from "hammerjs";
import cornerstone from "cornerstone-core";
import cornerstoneMath from "cornerstone-math";
import cornerstoneTools from "cornerstone-tools";
import { ref, defineProps, onMounted, watch } from "vue";
import cornerstoneWebImageLoader from "cornerstone-web-image-loader";

const props = defineProps({
  imageUrl: String,
});

const loaded = ref(false);
const imageIds = [
  "http://localhoat:8080/01/01.jpg",
  "http://localhoat:8080/01/02.jpg",
  "http://localhoat:8080/01/03.jpg",
  "http://localhoat:8080/01/04.jpg",
  "http://localhoat:8080/01/05.jpg",
  "http://localhoat:8080/01/06.jpg",
  "http://localhoat:8080/01/07.jpg",
  "http://localhoat:8080/01/08.jpg",
  "http://localhoat:8080/01/09.jpg",
  "http://localhoat:8080/01/10.jpg",
  "http://localhoat:8080/01/11.jpg",
];
console.log(imageIds);

const tempData = [
  {
    visible: true,
    active: false,
    invalidated: false,
    handles: {
      points: [
        {
          x: 543.596214511041,
          y: 231.2933753943218,
          highlight: true,
          active: true,
          lines: [
            {
              x: 544.6056782334384,
              y: 231.2933753943218,
            },
          ],
        },
        {
          x: 544.6056782334384,
          y: 231.2933753943218,
          highlight: true,
          active: true,
          lines: [
            {
              x: 544.6056782334384,
              y: 232.30283911671927,
            },
          ],
        },
        {
          x: 544.6056782334384,
          y: 232.30283911671927,
          highlight: true,
          active: true,
          lines: [
            {
              x: 545.615141955836,
              y: 232.30283911671927,
            },
          ],
        },
        {
          x: 545.615141955836,
          y: 232.30283911671927,
          highlight: true,
          active: true,
          lines: [
            {
              x: 545.615141955836,
              y: 233.31230283911674,
            },
          ],
        },
        {
          x: 545.615141955836,
          y: 233.31230283911674,
          highlight: true,
          active: true,
          lines: [
            {
              x: 546.6246056782334,
              y: 233.31230283911674,
            },
          ],
        },
        {
          x: 546.6246056782334,
          y: 233.31230283911674,
          highlight: true,
          active: true,
          lines: [
            {
              x: 546.6246056782334,
              y: 234.3217665615142,
            },
          ],
        },
        {
          x: 546.6246056782334,
          y: 234.3217665615142,
          highlight: true,
          active: true,
          lines: [
            {
              x: 547.6340694006309,
              y: 234.3217665615142,
            },
          ],
        },
        {
          x: 547.6340694006309,
          y: 234.3217665615142,
          highlight: true,
          active: true,
          lines: [
            {
              x: 746.4984227129337,
              y: 266.6246056782334,
            },
          ],
        },
        {
          x: 746.4984227129337,
          y: 266.6246056782334,
          highlight: true,
          active: true,
          lines: [
            {
              x: 746.4984227129337,
              y: 267.6340694006309,
            },
          ],
        },
        {
          x: 746.4984227129337,
          y: 267.6340694006309,
          highlight: true,
          active: true,
          lines: [
            {
              x: 746.4984227129337,
              y: 268.6435331230284,
            },
          ],
        },
        {
          x: 746.4984227129337,
          y: 268.6435331230284,
          highlight: true,
          active: true,
          lines: [
            {
              x: 747.5078864353312,
              y: 268.6435331230284,
            },
          ],
        },
        {
          x: 747.5078864353312,
          y: 268.6435331230284,
          highlight: true,
          active: true,
          lines: [
            {
              x: 747.5078864353312,
              y: 269.6529968454259,
            },
          ],
        },
        {
          x: 747.5078864353312,
          y: 269.6529968454259,
          highlight: true,
          active: true,
          lines: [
            {
              x: 746.4984227129337,
              y: 269.6529968454259,
            },
          ],
        },
        {
          x: 746.4984227129337,
          y: 269.6529968454259,
          highlight: true,
          active: true,
          lines: [
            {
              x: 830.2839116719242,
              y: 545.2365930599369,
            },
          ],
        },
        {
          x: 830.2839116719242,
          y: 545.2365930599369,
          highlight: true,
          active: true,
          lines: [
            {
              x: 829.2744479495268,
              y: 545.2365930599369,
            },
          ],
        },
        {
          x: 829.2744479495268,
          y: 545.2365930599369,
          highlight: true,
          active: true,
          lines: [
            {
              x: 829.2744479495268,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 829.2744479495268,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 828.2649842271293,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 828.2649842271293,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 827.2555205047319,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 827.2555205047319,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 826.2460567823343,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 826.2460567823343,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 825.2365930599368,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 825.2365930599368,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 824.2271293375394,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 824.2271293375394,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 823.2176656151419,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 823.2176656151419,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 822.2082018927445,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 822.2082018927445,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 821.1987381703469,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 821.1987381703469,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 819.179810725552,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 819.179810725552,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 818.1703470031546,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 818.1703470031546,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 816.1514195583595,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 816.1514195583595,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 815.1419558359621,
              y: 546.2460567823343,
            },
          ],
        },
        {
          x: 815.1419558359621,
          y: 546.2460567823343,
          highlight: true,
          active: true,
          lines: [
            {
              x: 813.1230283911672,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 813.1230283911672,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 812.1135646687696,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 812.1135646687696,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 810.0946372239747,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 810.0946372239747,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 808.0757097791798,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 808.0757097791798,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 807.0662460567822,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 807.0662460567822,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 805.0473186119873,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 805.0473186119873,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 803.0283911671924,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 803.0283911671924,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 802.0189274447949,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 802.0189274447949,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 800,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 800,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 797.981072555205,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 797.981072555205,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 796.9716088328075,
              y: 547.2555205047319,
            },
          ],
        },
        {
          x: 796.9716088328075,
          y: 547.2555205047319,
          highlight: true,
          active: true,
          lines: [
            {
              x: 477.981072555205,
              y: 461.4511041009464,
            },
          ],
        },
        {
          x: 477.981072555205,
          y: 461.4511041009464,
          highlight: true,
          active: true,
          lines: [
            {
              x: 456.782334384858,
              y: 299.93690851735016,
            },
          ],
        },
        {
          x: 456.782334384858,
          y: 299.93690851735016,
          highlight: true,
          active: true,
          lines: [
            {
              x: 457.7917981072555,
              y: 299.93690851735016,
            },
          ],
        },
        {
          x: 457.7917981072555,
          y: 299.93690851735016,
          highlight: true,
          active: true,
          lines: [
            {
              x: 543.596214511041,
              y: 231.2933753943218,
              highlight: true,
              active: true,
              lines: [
                {
                  x: 544.6056782334384,
                  y: 231.2933753943218,
                },
              ],
            },
          ],
        },
      ],
      textBox: {
        active: false,
        hasMoved: false,
        movesIndependently: false,
        drawnIndependently: true,
        allowedOutsideImage: true,
        hasBoundingBox: true,
        x: 830.2839116719242,
        y: 389.2744479495268,
        boundingBox: {
          width: 174.546875,
          height: 26,
          left: 822.4999999999999,
          top: 468.5,
        },
      },
      invalidHandlePlacement: false,
    },
    uuid: "482b6399-f392-4da4-8647-28e3b93cfec5",
    canComplete: false,
    highlight: false,
    polyBoundingBox: {
      left: 456.782334384858,
      top: 231.2933753943218,
      width: 373.5015772870662,
      height: 315.96214511041006,
    },
    area: 79186.28307575951,
  },
];

const selectedTool = ref();
const tools = ref([
  {
    label: "AngleTool",
    value: "Angle",
    enableValue: cornerstoneTools.AngleTool,
  },
  {
    label: "ArrowAnnotateTool",
    value: "ArrowAnnotate",
    enableValue: cornerstoneTools.ArrowAnnotateTool,
  },
  {
    label: "BidirectionalTool",
    value: "Bidirectional",
    enableValue: cornerstoneTools.BidirectionalTool,
  },
  {
    label: "BrushTool",
    value: "Brush",
    enableValue: cornerstoneTools.BrushTool,
  },
  {
    label: "CircleRoiTool",
    value: "CircleRoi",
    enableValue: cornerstoneTools.CircleRoiTool,
  },
  {
    label: "CircleScissorsTool",
    value: "CircleScissors",
    enableValue: cornerstoneTools.CircleScissorsTool,
  },
  {
    label: "CobbAngleTool",
    value: "CobbAngle",
    enableValue: cornerstoneTools.CobbAngleTool,
  },
  {
    label: "CorrectionScissorsTool",
    value: "CorrectionScissors",
    enableValue: cornerstoneTools.CorrectionScissorsTool,
  },
  {
    label: "CrosshairsTool",
    value: "Crosshairs",
    enableValue: cornerstoneTools.CrosshairsTool,
  },
  {
    label: "DoubleTapFitToWindowTool",
    value: "DoubleTapFitToWindow",
    enableValue: cornerstoneTools.DoubleTapFitToWindowTool,
  },
  {
    label: "DragProbeTool",
    value: "DragProbe",
    enableValue: cornerstoneTools.DragProbeTool,
  },
  {
    label: "EllipticalRoiTool",
    value: "EllipticalRoi",
    enableValue: cornerstoneTools.EllipticalRoiTool,
  },
  {
    label: "EraserTool",
    value: "Eraser",
    enableValue: cornerstoneTools.EraserTool,
  },
  {
    label: "FreehandRoiSculptorTool",
    value: "FreehandRoiSculptor",
    enableValue: cornerstoneTools.FreehandRoiSculptorTool,
  },
  {
    label: "FreehandRoiTool",
    value: "FreehandRoi",
    enableValue: cornerstoneTools.FreehandRoiTool,
  },
  {
    label: "FreehandScissorsTool",
    value: "FreehandScissors",
    enableValue: cornerstoneTools.FreehandScissorsTool,
  },
  {
    label: "RectangleRoiTool",
    value: "RectangleRoi",
    enableValue: cornerstoneTools.RectangleRoiTool,
  },
  {
    label: "ZoomMouseWheelTool",
    value: "ZoomMouseWheel",
    enableValue: cornerstoneTools.ZoomMouseWheelTool,
  },
]);
cornerstoneTools.external.Hammer = Hammer;
cornerstoneTools.external.cornerstone = cornerstone;
cornerstoneTools.external.cornerstoneMath = cornerstoneMath;
cornerstoneWebImageLoader.external.cornerstone = cornerstone;

cornerstoneWebImageLoader.configure({
  beforeSend: function (xhr) {
    console.log(xhr);
    // Add custom headers here (e.g. auth tokens)
    //xhr.setRequestHeader('x-auth-token', 'my auth token');
  },
});

const activateBrushTool = () => {
  cornerstoneTools.setToolActive("Brush", { mouseButtonMask: 1 });
};

const init = () => {
  cornerstoneTools.init([
    { showSVGCursors: true },
    {
      moduleName: "globalConfiguration",
      configuration: {
        showSVGCursors: true,
      },
    },
    {
      moduleName: "segmentation",
      configuration: {
        outlineWidth: 2,
      },
    },
  ]);

  // Set the tool font and font size
  const fontFamily =
    "Work Sans, Roboto, OpenSans, HelveticaNeue-Light, Helvetica Neue Light, Helvetica Neue, Helvetica, Arial, Lucida Grande, sans-serif";
  cornerstoneTools.toolStyle.setToolWidth(2);
  cornerstoneTools.textStyle.setFont(`16px ${fontFamily}`);
  cornerstoneTools.toolColors.setToolColor("rgb(255, 255, 0)");
  cornerstoneTools.toolColors.setActiveColor("rgb(0, 255, 0)");
};

// const getPolygonState = () => {
//   const element = document.getElementById("dicomImage");
//   const toolData = cornerstoneTools.getToolState(element, "FreehandRoi");
//   console.log(toolData, "toolDatatoolData");
//   //   toolData.data[0].handles.points.pop();
//   //   cornerstone.updateImage(element);
// };

const exportAnnotations = () => {
  // --- To serialize the tool states ---
  var element = document.getElementById("dicomImage");
  var allToolData = {};

  // Decide which tool types you want to serialize
  var toolTypes = ["FreehandRoi"];

  // Loop through all the tool types
  for (var i = 0; i < toolTypes.length; i++) {
    // Get the tool data for this tool type
    var toolType = toolTypes[i];
    var toolData = cornerstoneTools.getToolState(element, toolType);

    if (toolData !== undefined) {
      // Put it into an object
      allToolData[toolTypes[i]] = toolData;
    }
  }

  var toolDataString = JSON.stringify(allToolData);
  console.log(toolDataString, "toolDataStringtoolDataString");
};

const importAnnotations = () => {
  console.log(
    cornerstoneTools,

    "cornerstoneToolscornerstoneToolscornerstoneToolscornerstoneTools"
  );
  console.log(tempData, "tempDatatempDatatempData");
  // Try pasting this block into the allImageTools example:
  var element = document.getElementById("dicomImage");
  var toolDataString =
    '{"FreehandRoi":{"data":[{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":505.23659305993687,"y":291.86119873817034,"highlight":true,"active":true,"lines":[{"x":505.23659305993687,"y":290.8517350157729}]},{"x":505.23659305993687,"y":290.8517350157729,"highlight":true,"active":true,"lines":[{"x":505.23659305993687,"y":292.8706624605678}]},{"x":505.23659305993687,"y":292.8706624605678,"highlight":true,"active":true,"lines":[{"x":506.24605678233434,"y":292.8706624605678}]},{"x":506.24605678233434,"y":292.8706624605678,"highlight":true,"active":true,"lines":[{"x":506.24605678233434,"y":294.88958990536275}]},{"x":506.24605678233434,"y":294.88958990536275,"highlight":true,"active":true,"lines":[{"x":508.26498422712933,"y":296.90851735015775}]},{"x":508.26498422712933,"y":296.90851735015775,"highlight":true,"active":true,"lines":[{"x":508.26498422712933,"y":298.9274447949527}]},{"x":508.26498422712933,"y":298.9274447949527,"highlight":true,"active":true,"lines":[{"x":510.2839116719243,"y":298.9274447949527}]},{"x":510.2839116719243,"y":298.9274447949527,"highlight":true,"active":true,"lines":[{"x":510.2839116719243,"y":299.93690851735016}]},{"x":510.2839116719243,"y":299.93690851735016,"highlight":true,"active":true,"lines":[{"x":512.3028391167193,"y":301.9558359621451}]},{"x":512.3028391167193,"y":301.9558359621451,"highlight":true,"active":true,"lines":[{"x":512.3028391167193,"y":305.99369085173504}]},{"x":512.3028391167193,"y":305.99369085173504,"highlight":true,"active":true,"lines":[{"x":514.3217665615142,"y":308.01261829653}]},{"x":514.3217665615142,"y":308.01261829653,"highlight":true,"active":true,"lines":[{"x":514.3217665615142,"y":310.0315457413249}]},{"x":514.3217665615142,"y":310.0315457413249,"highlight":true,"active":true,"lines":[{"x":516.3406940063091,"y":314.06940063091486}]},{"x":516.3406940063091,"y":314.06940063091486,"highlight":true,"active":true,"lines":[{"x":516.3406940063091,"y":316.0883280757098}]},{"x":516.3406940063091,"y":316.0883280757098,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":318.10725552050474}]},{"x":518.3596214511041,"y":318.10725552050474,"highlight":true,"active":true,"lines":[{"x":521.3880126182964,"y":323.15457413249214}]},{"x":521.3880126182964,"y":323.15457413249214,"highlight":true,"active":true,"lines":[{"x":523.4069400630915,"y":325.1735015772871}]},{"x":523.4069400630915,"y":325.1735015772871,"highlight":true,"active":true,"lines":[{"x":643.5331230283912,"y":671.4195583596214}]},{"x":643.5331230283912,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":641.5141955835962,"y":671.4195583596214}]},{"x":641.5141955835962,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":640.5047318611987,"y":671.4195583596214}]},{"x":640.5047318611987,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":638.4858044164038,"y":671.4195583596214}]},{"x":638.4858044164038,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":638.4858044164038,"y":672.429022082019}]},{"x":638.4858044164038,"y":672.429022082019,"highlight":true,"active":true,"lines":[{"x":637.4763406940062,"y":672.429022082019}]},{"x":637.4763406940062,"y":672.429022082019,"highlight":true,"active":true,"lines":[{"x":635.4574132492113,"y":672.429022082019}]},{"x":635.4574132492113,"y":672.429022082019,"highlight":true,"active":true,"lines":[{"x":635.4574132492113,"y":674.4479495268139}]},{"x":635.4574132492113,"y":674.4479495268139,"highlight":true,"active":true,"lines":[{"x":634.4479495268139,"y":675.4574132492113}]},{"x":634.4479495268139,"y":675.4574132492113,"highlight":true,"active":true,"lines":[{"x":634.4479495268139,"y":676.4668769716088}]},{"x":634.4479495268139,"y":676.4668769716088,"highlight":true,"active":true,"lines":[{"x":634.4479495268139,"y":677.4763406940062}]},{"x":634.4479495268139,"y":677.4763406940062,"highlight":true,"active":true,"lines":[{"x":633.4384858044164,"y":677.4763406940062}]},{"x":633.4384858044164,"y":677.4763406940062,"highlight":true,"active":true,"lines":[{"x":632.429022082019,"y":676.4668769716088}]},{"x":632.429022082019,"y":676.4668769716088,"highlight":true,"active":true,"lines":[{"x":631.4195583596214,"y":676.4668769716088}]},{"x":631.4195583596214,"y":676.4668769716088,"highlight":true,"active":true,"lines":[{"x":630.4100946372239,"y":676.4668769716088}]},{"x":630.4100946372239,"y":676.4668769716088,"highlight":true,"active":true,"lines":[{"x":624.3533123028391,"y":675.4574132492113}]},{"x":624.3533123028391,"y":675.4574132492113,"highlight":true,"active":true,"lines":[{"x":623.3438485804417,"y":673.4384858044164}]},{"x":623.3438485804417,"y":673.4384858044164,"highlight":true,"active":true,"lines":[{"x":621.3249211356466,"y":673.4384858044164}]},{"x":621.3249211356466,"y":673.4384858044164,"highlight":true,"active":true,"lines":[{"x":620.3154574132492,"y":673.4384858044164}]},{"x":620.3154574132492,"y":673.4384858044164,"highlight":true,"active":true,"lines":[{"x":618.2965299684543,"y":673.4384858044164}]},{"x":618.2965299684543,"y":673.4384858044164,"highlight":true,"active":true,"lines":[{"x":616.2776025236593,"y":671.4195583596214}]},{"x":616.2776025236593,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":612.2397476340693,"y":671.4195583596214}]},{"x":612.2397476340693,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":610.2208201892744,"y":671.4195583596214}]},{"x":610.2208201892744,"y":671.4195583596214,"highlight":true,"active":true,"lines":[{"x":608.2018927444794,"y":669.4006309148265}]},{"x":608.2018927444794,"y":669.4006309148265,"highlight":true,"active":true,"lines":[{"x":607.192429022082,"y":669.4006309148265}]},{"x":607.192429022082,"y":669.4006309148265,"highlight":true,"active":true,"lines":[{"x":605.1735015772871,"y":667.3817034700315}]},{"x":605.1735015772871,"y":667.3817034700315,"highlight":true,"active":true,"lines":[{"x":601.1356466876971,"y":665.3627760252366}]},{"x":601.1356466876971,"y":665.3627760252366,"highlight":true,"active":true,"lines":[{"x":189.2744479495268,"y":532.1135646687698}]},{"x":189.2744479495268,"y":532.1135646687698,"highlight":true,"active":true,"lines":[{"x":189.2744479495268,"y":531.1041009463722}]},{"x":189.2744479495268,"y":531.1041009463722,"highlight":true,"active":true,"lines":[{"x":190.28391167192427,"y":531.1041009463722}]},{"x":190.28391167192427,"y":531.1041009463722,"highlight":true,"active":true,"lines":[{"x":190.28391167192427,"y":530.0946372239747}]},{"x":190.28391167192427,"y":530.0946372239747,"highlight":true,"active":true,"lines":[{"x":204.41640378548894,"y":382.7129337539432}]},{"x":204.41640378548894,"y":382.7129337539432,"highlight":true,"active":true,"lines":[{"x":205.42586750788644,"y":382.7129337539432}]},{"x":205.42586750788644,"y":382.7129337539432,"highlight":true,"active":true,"lines":[{"x":205.42586750788644,"y":381.70347003154575}]},{"x":205.42586750788644,"y":381.70347003154575,"highlight":true,"active":true,"lines":[{"x":206.4353312302839,"y":381.70347003154575}]},{"x":206.4353312302839,"y":381.70347003154575,"highlight":true,"active":true,"lines":[{"x":206.4353312302839,"y":380.6940063091483}]},{"x":206.4353312302839,"y":380.6940063091483,"highlight":true,"active":true,"lines":[{"x":207.44479495268138,"y":380.6940063091483}]},{"x":207.44479495268138,"y":380.6940063091483,"highlight":true,"active":true,"lines":[{"x":208.45425867507885,"y":380.6940063091483}]},{"x":208.45425867507885,"y":380.6940063091483,"highlight":true,"active":true,"lines":[{"x":208.45425867507885,"y":378.67507886435334}]},{"x":208.45425867507885,"y":378.67507886435334,"highlight":true,"active":true,"lines":[{"x":208.45425867507885,"y":377.6656151419558}]},{"x":208.45425867507885,"y":377.6656151419558,"highlight":true,"active":true,"lines":[{"x":208.45425867507885,"y":376.65615141955834}]},{"x":208.45425867507885,"y":376.65615141955834,"highlight":true,"active":true,"lines":[{"x":208.45425867507885,"y":375.64668769716087}]},{"x":208.45425867507885,"y":375.64668769716087,"highlight":true,"active":true,"lines":[{"x":209.46372239747632,"y":375.64668769716087}]},{"x":209.46372239747632,"y":375.64668769716087,"highlight":true,"active":true,"lines":[{"x":210.47318611987382,"y":375.64668769716087}]},{"x":210.47318611987382,"y":375.64668769716087,"highlight":true,"active":true,"lines":[{"x":210.47318611987382,"y":374.6372239747634}]},{"x":210.47318611987382,"y":374.6372239747634,"highlight":true,"active":true,"lines":[{"x":211.4826498422713,"y":374.6372239747634}]},{"x":211.4826498422713,"y":374.6372239747634,"highlight":true,"active":true,"lines":[{"x":212.49211356466876,"y":373.62776025236593}]},{"x":212.49211356466876,"y":373.62776025236593,"highlight":true,"active":true,"lines":[{"x":212.49211356466876,"y":372.61829652996846}]},{"x":212.49211356466876,"y":372.61829652996846,"highlight":true,"active":true,"lines":[{"x":212.49211356466876,"y":371.608832807571}]},{"x":212.49211356466876,"y":371.608832807571,"highlight":true,"active":true,"lines":[{"x":212.49211356466876,"y":370.5993690851735}]},{"x":212.49211356466876,"y":370.5993690851735,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":370.5993690851735}]},{"x":213.50157728706623,"y":370.5993690851735,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":368.5804416403785}]},{"x":213.50157728706623,"y":368.5804416403785,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":366.5615141955836}]},{"x":213.50157728706623,"y":366.5615141955836,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":365.5520504731861}]},{"x":213.50157728706623,"y":365.5520504731861,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":364.54258675078864}]},{"x":213.50157728706623,"y":364.54258675078864,"highlight":true,"active":true,"lines":[{"x":213.50157728706623,"y":363.5331230283912}]},{"x":213.50157728706623,"y":363.5331230283912,"highlight":true,"active":true,"lines":[{"x":215.5205047318612,"y":363.5331230283912}]},{"x":215.5205047318612,"y":363.5331230283912,"highlight":true,"active":true,"lines":[{"x":215.5205047318612,"y":361.51419558359623}]},{"x":215.5205047318612,"y":361.51419558359623,"highlight":true,"active":true,"lines":[{"x":217.53943217665613,"y":359.49526813880124}]},{"x":217.53943217665613,"y":359.49526813880124,"highlight":true,"active":true,"lines":[{"x":217.53943217665613,"y":358.48580441640377}]},{"x":217.53943217665613,"y":358.48580441640377,"highlight":true,"active":true,"lines":[{"x":218.5488958990536,"y":356.4668769716088}]},{"x":218.5488958990536,"y":356.4668769716088,"highlight":true,"active":true,"lines":[{"x":219.5583596214511,"y":355.45741324921136}]},{"x":219.5583596214511,"y":355.45741324921136,"highlight":true,"active":true,"lines":[{"x":220.56782334384857,"y":355.45741324921136}]},{"x":220.56782334384857,"y":355.45741324921136,"highlight":true,"active":true,"lines":[{"x":220.56782334384857,"y":354.4479495268139}]},{"x":220.56782334384857,"y":354.4479495268139,"highlight":true,"active":true,"lines":[{"x":224.60567823343848,"y":350.41009463722395}]},{"x":224.60567823343848,"y":350.41009463722395,"highlight":true,"active":true,"lines":[{"x":226.62460567823342,"y":348.391167192429}]},{"x":226.62460567823342,"y":348.391167192429,"highlight":true,"active":true,"lines":[{"x":228.6435331230284,"y":347.38170347003154}]},{"x":228.6435331230284,"y":347.38170347003154,"highlight":true,"active":true,"lines":[{"x":228.6435331230284,"y":345.3627760252366}]},{"x":228.6435331230284,"y":345.3627760252366,"highlight":true,"active":true,"lines":[{"x":229.65299684542586,"y":343.34384858044166}]},{"x":229.65299684542586,"y":343.34384858044166,"highlight":true,"active":true,"lines":[{"x":231.6719242902208,"y":341.32492113564666}]},{"x":231.6719242902208,"y":341.32492113564666,"highlight":true,"active":true,"lines":[{"x":231.6719242902208,"y":339.3059936908517}]},{"x":231.6719242902208,"y":339.3059936908517,"highlight":true,"active":true,"lines":[{"x":233.69085173501577,"y":337.2870662460568}]},{"x":233.69085173501577,"y":337.2870662460568,"highlight":true,"active":true,"lines":[{"x":233.69085173501577,"y":335.26813880126184}]},{"x":233.69085173501577,"y":335.26813880126184,"highlight":true,"active":true,"lines":[{"x":235.7097791798107,"y":334.25867507886437}]},{"x":235.7097791798107,"y":334.25867507886437,"highlight":true,"active":true,"lines":[{"x":235.7097791798107,"y":332.2397476340694}]},{"x":235.7097791798107,"y":332.2397476340694,"highlight":true,"active":true,"lines":[{"x":237.72870662460568,"y":332.2397476340694}]},{"x":237.72870662460568,"y":332.2397476340694,"highlight":true,"active":true,"lines":[{"x":237.72870662460568,"y":330.22082018927443}]},{"x":237.72870662460568,"y":330.22082018927443,"highlight":true,"active":true,"lines":[{"x":240.7570977917981,"y":328.2018927444795}]},{"x":240.7570977917981,"y":328.2018927444795,"highlight":true,"active":true,"lines":[{"x":240.7570977917981,"y":327.192429022082}]},{"x":240.7570977917981,"y":327.192429022082,"highlight":true,"active":true,"lines":[{"x":242.77602523659306,"y":327.192429022082}]},{"x":242.77602523659306,"y":327.192429022082,"highlight":true,"active":true,"lines":[{"x":242.77602523659306,"y":323.15457413249214}]},{"x":242.77602523659306,"y":323.15457413249214,"highlight":true,"active":true,"lines":[{"x":244.794952681388,"y":321.13564668769715}]},{"x":244.794952681388,"y":321.13564668769715,"highlight":true,"active":true,"lines":[{"x":246.81388012618294,"y":319.1167192429022}]},{"x":246.81388012618294,"y":319.1167192429022,"highlight":true,"active":true,"lines":[{"x":246.81388012618294,"y":317.09779179810727}]},{"x":246.81388012618294,"y":317.09779179810727,"highlight":true,"active":true,"lines":[{"x":248.8328075709779,"y":315.0788643533123}]},{"x":248.8328075709779,"y":315.0788643533123,"highlight":true,"active":true,"lines":[{"x":248.8328075709779,"y":313.05993690851733}]},{"x":248.8328075709779,"y":313.05993690851733,"highlight":true,"active":true,"lines":[{"x":250.85173501577285,"y":313.05993690851733}]},{"x":250.85173501577285,"y":313.05993690851733,"highlight":true,"active":true,"lines":[{"x":250.85173501577285,"y":312.05047318611986}]},{"x":250.85173501577285,"y":312.05047318611986,"highlight":true,"active":true,"lines":[{"x":250.85173501577285,"y":310.0315457413249}]},{"x":250.85173501577285,"y":310.0315457413249,"highlight":true,"active":true,"lines":[{"x":250.85173501577285,"y":308.01261829653}]},{"x":250.85173501577285,"y":308.01261829653,"highlight":true,"active":true,"lines":[{"x":250.85173501577285,"y":307.0031545741325}]},{"x":250.85173501577285,"y":307.0031545741325,"highlight":true,"active":true,"lines":[{"x":251.86119873817034,"y":304.98422712933757}]},{"x":251.86119873817034,"y":304.98422712933757,"highlight":true,"active":true,"lines":[{"x":251.86119873817034,"y":302.9652996845426}]},{"x":251.86119873817034,"y":302.9652996845426,"highlight":true,"active":true,"lines":[{"x":253.88012618296528,"y":300.94637223974763}]},{"x":253.88012618296528,"y":300.94637223974763,"highlight":true,"active":true,"lines":[{"x":254.88958990536275,"y":299.93690851735016}]},{"x":254.88958990536275,"y":299.93690851735016,"highlight":true,"active":true,"lines":[{"x":255.89905362776022,"y":298.9274447949527}]},{"x":255.89905362776022,"y":298.9274447949527,"highlight":true,"active":true,"lines":[{"x":257.91798107255516,"y":297.9179810725552}]},{"x":257.91798107255516,"y":297.9179810725552,"highlight":true,"active":true,"lines":[{"x":257.91798107255516,"y":295.8990536277603}]},{"x":257.91798107255516,"y":295.8990536277603,"highlight":true,"active":true,"lines":[{"x":258.9274447949527,"y":294.88958990536275}]},{"x":258.9274447949527,"y":294.88958990536275,"highlight":true,"active":true,"lines":[{"x":258.9274447949527,"y":292.8706624605678}]},{"x":258.9274447949527,"y":292.8706624605678,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":291.86119873817034}]},{"x":260.94637223974763,"y":291.86119873817034,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":289.8422712933754}]},{"x":260.94637223974763,"y":289.8422712933754,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":288.83280757097793}]},{"x":260.94637223974763,"y":288.83280757097793,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":287.82334384858046}]},{"x":260.94637223974763,"y":287.82334384858046,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":286.813880126183}]},{"x":260.94637223974763,"y":286.813880126183,"highlight":true,"active":true,"lines":[{"x":260.94637223974763,"y":285.80441640378547}]},{"x":260.94637223974763,"y":285.80441640378547,"highlight":true,"active":true,"lines":[{"x":261.9558359621451,"y":285.80441640378547}]},{"x":261.9558359621451,"y":285.80441640378547,"highlight":true,"active":true,"lines":[{"x":261.9558359621451,"y":283.7854889589905}]},{"x":261.9558359621451,"y":283.7854889589905,"highlight":true,"active":true,"lines":[{"x":261.9558359621451,"y":282.77602523659306}]},{"x":261.9558359621451,"y":282.77602523659306,"highlight":true,"active":true,"lines":[{"x":505.23659305993687,"y":291.86119873817034,"highlight":true,"active":true,"lines":[{"x":505.23659305993687,"y":290.8517350157729}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":643.5331230283912,"y":480.1261829652997,"boundingBox":{"width":182.2578125,"height":26,"left":637.5,"top":558.5}},"invalidHandlePlacement":false},"uuid":"b71b8be4-de0c-46c8-8344-4ba8506a03f0","canComplete":false,"highlight":false,"polyBoundingBox":{"left":189.2744479495268,"top":282.77602523659306,"width":454.25867507886437,"height":394.7003154574132},"area":113344.24265342468},{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":716.2145110410095,"y":214.1324921135647,"highlight":true,"active":true,"lines":[{"x":716.2145110410095,"y":213.12302839116722}]},{"x":716.2145110410095,"y":213.12302839116722,"highlight":true,"active":true,"lines":[{"x":836.3406940063091,"y":354.4479495268139}]},{"x":836.3406940063091,"y":354.4479495268139,"highlight":true,"active":true,"lines":[{"x":837.3501577287066,"y":354.4479495268139}]},{"x":837.3501577287066,"y":354.4479495268139,"highlight":true,"active":true,"lines":[{"x":837.3501577287066,"y":355.45741324921136}]},{"x":837.3501577287066,"y":355.45741324921136,"highlight":true,"active":true,"lines":[{"x":838.3596214511041,"y":355.45741324921136}]},{"x":838.3596214511041,"y":355.45741324921136,"highlight":true,"active":true,"lines":[{"x":819.179810725552,"y":357.4763406940063}]},{"x":819.179810725552,"y":357.4763406940063,"highlight":true,"active":true,"lines":[{"x":579.9369085173502,"y":345.3627760252366}]},{"x":579.9369085173502,"y":345.3627760252366,"highlight":true,"active":true,"lines":[{"x":580.9463722397476,"y":345.3627760252366}]},{"x":580.9463722397476,"y":345.3627760252366,"highlight":true,"active":true,"lines":[{"x":580.9463722397476,"y":344.35331230283913}]},{"x":580.9463722397476,"y":344.35331230283913,"highlight":true,"active":true,"lines":[{"x":580.9463722397476,"y":343.34384858044166}]},{"x":580.9463722397476,"y":343.34384858044166,"highlight":true,"active":true,"lines":[{"x":578.9274447949526,"y":343.34384858044166}]},{"x":578.9274447949526,"y":343.34384858044166,"highlight":true,"active":true,"lines":[{"x":578.9274447949526,"y":341.32492113564666}]},{"x":578.9274447949526,"y":341.32492113564666,"highlight":true,"active":true,"lines":[{"x":577.9179810725552,"y":341.32492113564666}]},{"x":577.9179810725552,"y":341.32492113564666,"highlight":true,"active":true,"lines":[{"x":577.9179810725552,"y":340.3154574132492}]},{"x":577.9179810725552,"y":340.3154574132492,"highlight":true,"active":true,"lines":[{"x":577.9179810725552,"y":339.3059936908517}]},{"x":577.9179810725552,"y":339.3059936908517,"highlight":true,"active":true,"lines":[{"x":577.9179810725552,"y":338.29652996845425}]},{"x":577.9179810725552,"y":338.29652996845425,"highlight":true,"active":true,"lines":[{"x":576.9085173501577,"y":338.29652996845425}]},{"x":576.9085173501577,"y":338.29652996845425,"highlight":true,"active":true,"lines":[{"x":515.3312302839116,"y":165.6782334384858}]},{"x":515.3312302839116,"y":165.6782334384858,"highlight":true,"active":true,"lines":[{"x":516.3406940063091,"y":164.66876971608832}]},{"x":516.3406940063091,"y":164.66876971608832,"highlight":true,"active":true,"lines":[{"x":517.3501577287066,"y":164.66876971608832}]},{"x":517.3501577287066,"y":164.66876971608832,"highlight":true,"active":true,"lines":[{"x":716.2145110410095,"y":214.1324921135647,"highlight":true,"active":true,"lines":[{"x":716.2145110410095,"y":213.12302839116722}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":838.3596214511041,"y":440.4416403785489,"boundingBox":{"width":174.546875,"height":26,"left":830.5,"top":519.1875}},"invalidHandlePlacement":false},"uuid":"bc2291a6-3cfe-4e08-b4ec-340d32bc1724","canComplete":false,"highlight":false,"polyBoundingBox":{"left":515.3312302839116,"top":164.66876971608832,"width":323.02839116719247,"height":551.5457413249212},"area":34654.220859994566},{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":772.7444794952681,"y":163.65930599369085,"highlight":true,"active":true,"lines":[{"x":882.776025236593,"y":311.0410094637224}]},{"x":882.776025236593,"y":311.0410094637224,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":343.34384858044166}]},{"x":518.3596214511041,"y":343.34384858044166,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":342.3343848580442}]},{"x":518.3596214511041,"y":342.3343848580442,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":341.32492113564666}]},{"x":518.3596214511041,"y":341.32492113564666,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":340.3154574132492}]},{"x":518.3596214511041,"y":340.3154574132492,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":339.3059936908517}]},{"x":518.3596214511041,"y":339.3059936908517,"highlight":true,"active":true,"lines":[{"x":518.3596214511041,"y":338.29652996845425}]},{"x":518.3596214511041,"y":338.29652996845425,"highlight":true,"active":true,"lines":[{"x":499.17981072555204,"y":156.5930599369085}]},{"x":499.17981072555204,"y":156.5930599369085,"highlight":true,"active":true,"lines":[{"x":772.7444794952681,"y":163.65930599369085,"highlight":true,"active":true,"lines":[{"x":882.776025236593,"y":311.0410094637224}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":882.776025236593,"y":464.6687697160883,"boundingBox":{"width":174.546875,"height":26,"left":874.4999999999999,"top":543.1875}},"invalidHandlePlacement":false},"uuid":"51b5fb44-90c8-458d-967c-3683463ff0c3","canComplete":false,"highlight":false,"polyBoundingBox":{"left":499.17981072555204,"top":156.5930599369085,"width":383.59621451104096,"height":616.1514195583596},"area":54059.36172118339},{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":836.3406940063091,"y":141.4511041009464,"highlight":true,"active":true,"lines":[{"x":963.5331230283911,"y":390.78864353312304}]},{"x":963.5331230283911,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":962.5236593059936,"y":390.78864353312304}]},{"x":962.5236593059936,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":961.5141955835961,"y":390.78864353312304}]},{"x":961.5141955835961,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":960.5047318611987,"y":390.78864353312304}]},{"x":960.5047318611987,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":958.4858044164038,"y":390.78864353312304}]},{"x":958.4858044164038,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":957.4763406940062,"y":390.78864353312304}]},{"x":957.4763406940062,"y":390.78864353312304,"highlight":true,"active":true,"lines":[{"x":956.4668769716088,"y":391.7981072555205}]},{"x":956.4668769716088,"y":391.7981072555205,"highlight":true,"active":true,"lines":[{"x":955.4574132492113,"y":391.7981072555205}]},{"x":955.4574132492113,"y":391.7981072555205,"highlight":true,"active":true,"lines":[{"x":497.16088328075705,"y":403.9116719242902}]},{"x":497.16088328075705,"y":403.9116719242902,"highlight":true,"active":true,"lines":[{"x":497.16088328075705,"y":402.90220820189273}]},{"x":497.16088328075705,"y":402.90220820189273,"highlight":true,"active":true,"lines":[{"x":497.16088328075705,"y":401.89274447949526}]},{"x":497.16088328075705,"y":401.89274447949526,"highlight":true,"active":true,"lines":[{"x":496.1514195583596,"y":401.89274447949526}]},{"x":496.1514195583596,"y":401.89274447949526,"highlight":true,"active":true,"lines":[{"x":496.1514195583596,"y":400.8832807570978}]},{"x":496.1514195583596,"y":400.8832807570978,"highlight":true,"active":true,"lines":[{"x":494.13249211356464,"y":399.8738170347003}]},{"x":494.13249211356464,"y":399.8738170347003,"highlight":true,"active":true,"lines":[{"x":494.13249211356464,"y":398.86435331230285}]},{"x":494.13249211356464,"y":398.86435331230285,"highlight":true,"active":true,"lines":[{"x":494.13249211356464,"y":397.8548895899054}]},{"x":494.13249211356464,"y":397.8548895899054,"highlight":true,"active":true,"lines":[{"x":494.13249211356464,"y":396.84542586750786}]},{"x":494.13249211356464,"y":396.84542586750786,"highlight":true,"active":true,"lines":[{"x":494.13249211356464,"y":395.8359621451104}]},{"x":494.13249211356464,"y":395.8359621451104,"highlight":true,"active":true,"lines":[{"x":493.12302839116717,"y":393.81703470031545}]},{"x":493.12302839116717,"y":393.81703470031545,"highlight":true,"active":true,"lines":[{"x":493.12302839116717,"y":392.807570977918}]},{"x":493.12302839116717,"y":392.807570977918,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":392.807570977918}]},{"x":492.1135646687697,"y":392.807570977918,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":391.7981072555205}]},{"x":492.1135646687697,"y":391.7981072555205,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":388.7697160883281}]},{"x":492.1135646687697,"y":388.7697160883281,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":387.76025236593057}]},{"x":492.1135646687697,"y":387.76025236593057,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":386.7507886435331}]},{"x":492.1135646687697,"y":386.7507886435331,"highlight":true,"active":true,"lines":[{"x":492.1135646687697,"y":384.73186119873816}]},{"x":492.1135646687697,"y":384.73186119873816,"highlight":true,"active":true,"lines":[{"x":490.09463722397476,"y":382.7129337539432}]},{"x":490.09463722397476,"y":382.7129337539432,"highlight":true,"active":true,"lines":[{"x":488.07570977917976,"y":380.6940063091483}]},{"x":488.07570977917976,"y":380.6940063091483,"highlight":true,"active":true,"lines":[{"x":488.07570977917976,"y":378.67507886435334}]},{"x":488.07570977917976,"y":378.67507886435334,"highlight":true,"active":true,"lines":[{"x":486.0567823343848,"y":376.65615141955834}]},{"x":486.0567823343848,"y":376.65615141955834,"highlight":true,"active":true,"lines":[{"x":484.0378548895899,"y":374.6372239747634}]},{"x":484.0378548895899,"y":374.6372239747634,"highlight":true,"active":true,"lines":[{"x":484.0378548895899,"y":372.61829652996846}]},{"x":484.0378548895899,"y":372.61829652996846,"highlight":true,"active":true,"lines":[{"x":484.0378548895899,"y":371.608832807571}]},{"x":484.0378548895899,"y":371.608832807571,"highlight":true,"active":true,"lines":[{"x":482.01892744479494,"y":369.58990536277605}]},{"x":482.01892744479494,"y":369.58990536277605,"highlight":true,"active":true,"lines":[{"x":482.01892744479494,"y":367.57097791798105}]},{"x":482.01892744479494,"y":367.57097791798105,"highlight":true,"active":true,"lines":[{"x":482.01892744479494,"y":365.5520504731861}]},{"x":482.01892744479494,"y":365.5520504731861,"highlight":true,"active":true,"lines":[{"x":480,"y":357.4763406940063}]},{"x":480,"y":357.4763406940063,"highlight":true,"active":true,"lines":[{"x":480,"y":355.45741324921136}]},{"x":480,"y":355.45741324921136,"highlight":true,"active":true,"lines":[{"x":480,"y":353.4384858044164}]},{"x":480,"y":353.4384858044164,"highlight":true,"active":true,"lines":[{"x":480,"y":352.42902208201895}]},{"x":480,"y":352.42902208201895,"highlight":true,"active":true,"lines":[{"x":480,"y":350.41009463722395}]},{"x":480,"y":350.41009463722395,"highlight":true,"active":true,"lines":[{"x":480,"y":348.391167192429}]},{"x":480,"y":348.391167192429,"highlight":true,"active":true,"lines":[{"x":477.981072555205,"y":346.37223974763407}]},{"x":477.981072555205,"y":346.37223974763407,"highlight":true,"active":true,"lines":[{"x":477.981072555205,"y":345.3627760252366}]},{"x":477.981072555205,"y":345.3627760252366,"highlight":true,"active":true,"lines":[{"x":477.981072555205,"y":343.34384858044166}]},{"x":477.981072555205,"y":343.34384858044166,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":341.32492113564666}]},{"x":476.97160883280753,"y":341.32492113564666,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":339.3059936908517}]},{"x":476.97160883280753,"y":339.3059936908517,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":338.29652996845425}]},{"x":476.97160883280753,"y":338.29652996845425,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":334.25867507886437}]},{"x":476.97160883280753,"y":334.25867507886437,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":332.2397476340694}]},{"x":476.97160883280753,"y":332.2397476340694,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":328.2018927444795}]},{"x":476.97160883280753,"y":328.2018927444795,"highlight":true,"active":true,"lines":[{"x":476.97160883280753,"y":325.1735015772871}]},{"x":476.97160883280753,"y":325.1735015772871,"highlight":true,"active":true,"lines":[{"x":474.9526813880126,"y":323.15457413249214}]},{"x":474.9526813880126,"y":323.15457413249214,"highlight":true,"active":true,"lines":[{"x":474.9526813880126,"y":321.13564668769715}]},{"x":474.9526813880126,"y":321.13564668769715,"highlight":true,"active":true,"lines":[{"x":447.69716088328073,"y":107.12933753943217}]},{"x":447.69716088328073,"y":107.12933753943217,"highlight":true,"active":true,"lines":[{"x":447.69716088328073,"y":106.1198738170347}]},{"x":447.69716088328073,"y":106.1198738170347,"highlight":true,"active":true,"lines":[{"x":764.6687697160883,"y":63.7223974763407}]},{"x":764.6687697160883,"y":63.7223974763407,"highlight":true,"active":true,"lines":[{"x":836.3406940063091,"y":141.4511041009464,"highlight":true,"active":true,"lines":[{"x":963.5331230283911,"y":390.78864353312304}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":963.5331230283911,"y":450.0315457413249,"boundingBox":{"width":183.4453125,"height":26,"left":954.4999999999999,"top":528.6875}},"invalidHandlePlacement":false},"uuid":"5e64e631-ec63-4b5b-b787-49ec82f10ff7","canComplete":false,"highlight":false,"polyBoundingBox":{"left":447.69716088328073,"top":63.7223974763407,"width":515.8359621451103,"height":772.6182965299685},"area":131465.42208599945},{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":1070.5362776025236,"y":104.10094637223976,"highlight":true,"active":true,"lines":[{"x":1071.545741324921,"y":104.10094637223976}]},{"x":1071.545741324921,"y":104.10094637223976,"highlight":true,"active":true,"lines":[{"x":1072.5552050473186,"y":104.10094637223976}]},{"x":1072.5552050473186,"y":104.10094637223976,"highlight":true,"active":true,"lines":[{"x":1072.5552050473186,"y":103.09148264984226}]},{"x":1072.5552050473186,"y":103.09148264984226,"highlight":true,"active":true,"lines":[{"x":1169.4637223974762,"y":446.3091482649842}]},{"x":1169.4637223974762,"y":446.3091482649842,"highlight":true,"active":true,"lines":[{"x":1170.4731861198738,"y":448.3280757097792}]},{"x":1170.4731861198738,"y":448.3280757097792,"highlight":true,"active":true,"lines":[{"x":1170.4731861198738,"y":449.33753943217664}]},{"x":1170.4731861198738,"y":449.33753943217664,"highlight":true,"active":true,"lines":[{"x":1170.4731861198738,"y":450.34700315457417}]},{"x":1170.4731861198738,"y":450.34700315457417,"highlight":true,"active":true,"lines":[{"x":739.4321766561513,"y":477.60252365930603}]},{"x":739.4321766561513,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":738.4227129337539,"y":477.60252365930603}]},{"x":738.4227129337539,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":737.4132492113564,"y":477.60252365930603}]},{"x":737.4132492113564,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":735.3943217665615,"y":477.60252365930603}]},{"x":735.3943217665615,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":732.365930599369,"y":477.60252365930603}]},{"x":732.365930599369,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":731.3564668769716,"y":477.60252365930603}]},{"x":731.3564668769716,"y":477.60252365930603,"highlight":true,"active":true,"lines":[{"x":730.347003154574,"y":476.5930599369085}]},{"x":730.347003154574,"y":476.5930599369085,"highlight":true,"active":true,"lines":[{"x":729.3375394321766,"y":476.5930599369085}]},{"x":729.3375394321766,"y":476.5930599369085,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":476.5930599369085}]},{"x":728.3280757097791,"y":476.5930599369085,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":475.5835962145111}]},{"x":728.3280757097791,"y":475.5835962145111,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":474.57413249211356}]},{"x":728.3280757097791,"y":474.57413249211356,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":473.56466876971604}]},{"x":728.3280757097791,"y":473.56466876971604,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":472.5552050473186}]},{"x":728.3280757097791,"y":472.5552050473186,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":471.5457413249211}]},{"x":728.3280757097791,"y":471.5457413249211,"highlight":true,"active":true,"lines":[{"x":728.3280757097791,"y":470.5362776025237}]},{"x":728.3280757097791,"y":470.5362776025237,"highlight":true,"active":true,"lines":[{"x":726.3091482649842,"y":469.52681388012616}]},{"x":726.3091482649842,"y":469.52681388012616,"highlight":true,"active":true,"lines":[{"x":726.3091482649842,"y":468.51735015772874}]},{"x":726.3091482649842,"y":468.51735015772874,"highlight":true,"active":true,"lines":[{"x":565.8044164037855,"y":86.94006309148266}]},{"x":565.8044164037855,"y":86.94006309148266,"highlight":true,"active":true,"lines":[{"x":566.8138801261829,"y":85.93059936908519}]},{"x":566.8138801261829,"y":85.93059936908519,"highlight":true,"active":true,"lines":[{"x":864.6056782334384,"y":27.381703470031553}]},{"x":864.6056782334384,"y":27.381703470031553,"highlight":true,"active":true,"lines":[{"x":865.615141955836,"y":27.381703470031553}]},{"x":865.615141955836,"y":27.381703470031553,"highlight":true,"active":true,"lines":[{"x":1070.5362776025236,"y":104.10094637223976,"highlight":true,"active":true,"lines":[{"x":1071.545741324921,"y":104.10094637223976}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":1170.4731861198738,"y":548.9589905362775,"boundingBox":{"width":183.4453125,"height":26,"left":1159.5,"top":626.6874999999999}},"invalidHandlePlacement":false},"uuid":"d87b0b37-9324-4038-a859-638a45811af0","canComplete":false,"highlight":false,"polyBoundingBox":{"left":565.8044164037855,"top":27.381703470031553,"width":604.6687697160884,"height":1043.154574132492},"area":193077.73786185557},{"visible":true,"active":false,"invalidated":false,"handles":{"points":[{"x":401.2618296529968,"y":48.58044164037857,"highlight":true,"active":true,"lines":[{"x":401.2618296529968,"y":49.58990536277604}]},{"x":401.2618296529968,"y":49.58990536277604,"highlight":true,"active":true,"lines":[{"x":402.2712933753943,"y":49.58990536277604}]},{"x":402.2712933753943,"y":49.58990536277604,"highlight":true,"active":true,"lines":[{"x":403.28075709779176,"y":49.58990536277604}]},{"x":403.28075709779176,"y":49.58990536277604,"highlight":true,"active":true,"lines":[{"x":403.28075709779176,"y":48.58044164037857}]},{"x":403.28075709779176,"y":48.58044164037857,"highlight":true,"active":true,"lines":[{"x":441.64037854889585,"y":312.05047318611986}]},{"x":441.64037854889585,"y":312.05047318611986,"highlight":true,"active":true,"lines":[{"x":441.64037854889585,"y":311.0410094637224}]},{"x":441.64037854889585,"y":311.0410094637224,"highlight":true,"active":true,"lines":[{"x":487.0662460567823,"y":562.397476340694}]},{"x":487.0662460567823,"y":562.397476340694,"highlight":true,"active":true,"lines":[{"x":488.07570977917976,"y":562.397476340694}]},{"x":488.07570977917976,"y":562.397476340694,"highlight":true,"active":true,"lines":[{"x":299.3059936908517,"y":656.2776025236593}]},{"x":299.3059936908517,"y":656.2776025236593,"highlight":true,"active":true,"lines":[{"x":226.62460567823342,"y":494.7634069400631}]},{"x":226.62460567823342,"y":494.7634069400631,"highlight":true,"active":true,"lines":[{"x":118.61198738170346,"y":242.39747634069403}]},{"x":118.61198738170346,"y":242.39747634069403,"highlight":true,"active":true,"lines":[{"x":224.60567823343848,"y":129.33753943217664}]},{"x":224.60567823343848,"y":129.33753943217664,"highlight":true,"active":true,"lines":[{"x":262.9652996845426,"y":114.19558359621452}]},{"x":262.9652996845426,"y":114.19558359621452,"highlight":true,"active":true,"lines":[{"x":263.97476340694004,"y":114.19558359621452}]},{"x":263.97476340694004,"y":114.19558359621452,"highlight":true,"active":true,"lines":[{"x":263.97476340694004,"y":113.18611987381705}]},{"x":263.97476340694004,"y":113.18611987381705,"highlight":true,"active":true,"lines":[{"x":264.9842271293375,"y":113.18611987381705}]},{"x":264.9842271293375,"y":113.18611987381705,"highlight":true,"active":true,"lines":[{"x":264.9842271293375,"y":112.17665615141955}]},{"x":264.9842271293375,"y":112.17665615141955,"highlight":true,"active":true,"lines":[{"x":265.993690851735,"y":112.17665615141955}]},{"x":265.993690851735,"y":112.17665615141955,"highlight":true,"active":true,"lines":[{"x":265.993690851735,"y":111.16719242902208}]},{"x":265.993690851735,"y":111.16719242902208,"highlight":true,"active":true,"lines":[{"x":267.00315457413245,"y":111.16719242902208}]},{"x":267.00315457413245,"y":111.16719242902208,"highlight":true,"active":true,"lines":[{"x":268.01261829653,"y":111.16719242902208}]},{"x":268.01261829653,"y":111.16719242902208,"highlight":true,"active":true,"lines":[{"x":269.02208201892745,"y":111.16719242902208}]},{"x":269.02208201892745,"y":111.16719242902208,"highlight":true,"active":true,"lines":[{"x":270.0315457413249,"y":111.16719242902208}]},{"x":270.0315457413249,"y":111.16719242902208,"highlight":true,"active":true,"lines":[{"x":270.0315457413249,"y":109.14826498422714}]},{"x":270.0315457413249,"y":109.14826498422714,"highlight":true,"active":true,"lines":[{"x":271.0410094637224,"y":109.14826498422714}]},{"x":271.0410094637224,"y":109.14826498422714,"highlight":true,"active":true,"lines":[{"x":272.05047318611986,"y":108.13880126182964}]},{"x":272.05047318611986,"y":108.13880126182964,"highlight":true,"active":true,"lines":[{"x":274.0694006309148,"y":107.12933753943217}]},{"x":274.0694006309148,"y":107.12933753943217,"highlight":true,"active":true,"lines":[{"x":274.0694006309148,"y":106.1198738170347}]},{"x":274.0694006309148,"y":106.1198738170347,"highlight":true,"active":true,"lines":[{"x":275.07886435331227,"y":104.10094637223976}]},{"x":275.07886435331227,"y":104.10094637223976,"highlight":true,"active":true,"lines":[{"x":277.09779179810727,"y":102.08201892744479}]},{"x":277.09779179810727,"y":102.08201892744479,"highlight":true,"active":true,"lines":[{"x":279.1167192429022,"y":100.06309148264985}]},{"x":279.1167192429022,"y":100.06309148264985,"highlight":true,"active":true,"lines":[{"x":281.13564668769715,"y":100.06309148264985}]},{"x":281.13564668769715,"y":100.06309148264985,"highlight":true,"active":true,"lines":[{"x":283.1545741324921,"y":98.04416403785488}]},{"x":283.1545741324921,"y":98.04416403785488,"highlight":true,"active":true,"lines":[{"x":285.173501577287,"y":96.02523659305994}]},{"x":285.173501577287,"y":96.02523659305994,"highlight":true,"active":true,"lines":[{"x":287.192429022082,"y":94.00630914826498}]},{"x":287.192429022082,"y":94.00630914826498,"highlight":true,"active":true,"lines":[{"x":291.2302839116719,"y":94.00630914826498}]},{"x":291.2302839116719,"y":94.00630914826498,"highlight":true,"active":true,"lines":[{"x":293.24921135646684,"y":91.98738170347004}]},{"x":293.24921135646684,"y":91.98738170347004,"highlight":true,"active":true,"lines":[{"x":295.2681388012618,"y":89.96845425867507}]},{"x":295.2681388012618,"y":89.96845425867507,"highlight":true,"active":true,"lines":[{"x":299.3059936908517,"y":87.94952681388013}]},{"x":299.3059936908517,"y":87.94952681388013,"highlight":true,"active":true,"lines":[{"x":301.32492113564666,"y":85.93059936908519}]},{"x":301.32492113564666,"y":85.93059936908519,"highlight":true,"active":true,"lines":[{"x":303.3438485804416,"y":81.89274447949528}]},{"x":303.3438485804416,"y":81.89274447949528,"highlight":true,"active":true,"lines":[{"x":305.3627760252366,"y":79.87381703470031}]},{"x":305.3627760252366,"y":79.87381703470031,"highlight":true,"active":true,"lines":[{"x":307.38170347003154,"y":75.8359621451104}]},{"x":307.38170347003154,"y":75.8359621451104,"highlight":true,"active":true,"lines":[{"x":311.4195583596214,"y":73.81703470031546}]},{"x":311.4195583596214,"y":73.81703470031546,"highlight":true,"active":true,"lines":[{"x":313.43848580441636,"y":71.79810725552052}]},{"x":313.43848580441636,"y":71.79810725552052,"highlight":true,"active":true,"lines":[{"x":315.45741324921136,"y":69.77917981072555}]},{"x":315.45741324921136,"y":69.77917981072555,"highlight":true,"active":true,"lines":[{"x":319.49526813880124,"y":67.76025236593061}]},{"x":319.49526813880124,"y":67.76025236593061,"highlight":true,"active":true,"lines":[{"x":321.5141955835962,"y":65.74132492113564}]},{"x":321.5141955835962,"y":65.74132492113564,"highlight":true,"active":true,"lines":[{"x":325.5520504731861,"y":63.7223974763407}]},{"x":325.5520504731861,"y":63.7223974763407,"highlight":true,"active":true,"lines":[{"x":327.57097791798105,"y":61.703470031545734}]},{"x":327.57097791798105,"y":61.703470031545734,"highlight":true,"active":true,"lines":[{"x":329.589905362776,"y":59.684542586750794}]},{"x":329.589905362776,"y":59.684542586750794,"highlight":true,"active":true,"lines":[{"x":331.60883280757093,"y":57.665615141955826}]},{"x":331.60883280757093,"y":57.665615141955826,"highlight":true,"active":true,"lines":[{"x":335.64668769716087,"y":53.627760252365945}]},{"x":335.64668769716087,"y":53.627760252365945,"highlight":true,"active":true,"lines":[{"x":337.6656151419558,"y":51.60883280757098}]},{"x":337.6656151419558,"y":51.60883280757098,"highlight":true,"active":true,"lines":[{"x":339.68454258675075,"y":49.58990536277604}]},{"x":339.68454258675075,"y":49.58990536277604,"highlight":true,"active":true,"lines":[{"x":341.70347003154575,"y":47.57097791798107}]},{"x":341.70347003154575,"y":47.57097791798107,"highlight":true,"active":true,"lines":[{"x":343.7223974763407,"y":45.55205047318613}]},{"x":343.7223974763407,"y":45.55205047318613,"highlight":true,"active":true,"lines":[{"x":345.74132492113563,"y":43.53312302839116}]},{"x":345.74132492113563,"y":43.53312302839116,"highlight":true,"active":true,"lines":[{"x":347.76025236593057,"y":41.51419558359622}]},{"x":347.76025236593057,"y":41.51419558359622,"highlight":true,"active":true,"lines":[{"x":351.7981072555205,"y":39.49526813880128}]},{"x":351.7981072555205,"y":39.49526813880128,"highlight":true,"active":true,"lines":[{"x":353.81703470031545,"y":37.47634069400631}]},{"x":353.81703470031545,"y":37.47634069400631,"highlight":true,"active":true,"lines":[{"x":355.8359621451104,"y":35.45741324921137}]},{"x":355.8359621451104,"y":35.45741324921137,"highlight":true,"active":true,"lines":[{"x":357.8548895899053,"y":35.45741324921137}]},{"x":357.8548895899053,"y":35.45741324921137,"highlight":true,"active":true,"lines":[{"x":358.8643533123028,"y":33.4384858044164}]},{"x":358.8643533123028,"y":33.4384858044164,"highlight":true,"active":true,"lines":[{"x":360.8832807570978,"y":33.4384858044164}]},{"x":360.8832807570978,"y":33.4384858044164,"highlight":true,"active":true,"lines":[{"x":362.90220820189273,"y":33.4384858044164}]},{"x":362.90220820189273,"y":33.4384858044164,"highlight":true,"active":true,"lines":[{"x":364.9211356466877,"y":32.42902208201893}]},{"x":364.9211356466877,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":366.9400630914826,"y":32.42902208201893}]},{"x":366.9400630914826,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":367.9495268138801,"y":32.42902208201893}]},{"x":367.9495268138801,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":369.9684542586751,"y":32.42902208201893}]},{"x":369.9684542586751,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":369.9684542586751,"y":30.410094637223978}]},{"x":369.9684542586751,"y":30.410094637223978,"highlight":true,"active":true,"lines":[{"x":371.98738170347,"y":30.410094637223978}]},{"x":371.98738170347,"y":30.410094637223978,"highlight":true,"active":true,"lines":[{"x":372.9968454258675,"y":30.410094637223978}]},{"x":372.9968454258675,"y":30.410094637223978,"highlight":true,"active":true,"lines":[{"x":375.01577287066243,"y":28.391167192429023}]},{"x":375.01577287066243,"y":28.391167192429023,"highlight":true,"active":true,"lines":[{"x":377.03470031545737,"y":27.381703470031553}]},{"x":377.03470031545737,"y":27.381703470031553,"highlight":true,"active":true,"lines":[{"x":378.04416403785484,"y":25.3627760252366}]},{"x":378.04416403785484,"y":25.3627760252366,"highlight":true,"active":true,"lines":[{"x":378.04416403785484,"y":24.353312302839115}]},{"x":378.04416403785484,"y":24.353312302839115,"highlight":true,"active":true,"lines":[{"x":378.04416403785484,"y":22.334384858044174}]},{"x":378.04416403785484,"y":22.334384858044174,"highlight":true,"active":true,"lines":[{"x":380.06309148264984,"y":22.334384858044174}]},{"x":380.06309148264984,"y":22.334384858044174,"highlight":true,"active":true,"lines":[{"x":380.06309148264984,"y":21.32492113564669}]},{"x":380.06309148264984,"y":21.32492113564669,"highlight":true,"active":true,"lines":[{"x":381.0725552050473,"y":21.32492113564669}]},{"x":381.0725552050473,"y":21.32492113564669,"highlight":true,"active":true,"lines":[{"x":381.0725552050473,"y":20.31545741324922}]},{"x":381.0725552050473,"y":20.31545741324922,"highlight":true,"active":true,"lines":[{"x":382.0820189274448,"y":20.31545741324922}]},{"x":382.0820189274448,"y":20.31545741324922,"highlight":true,"active":true,"lines":[{"x":382.0820189274448,"y":19.305993690851736}]},{"x":382.0820189274448,"y":19.305993690851736,"highlight":true,"active":true,"lines":[{"x":383.09148264984225,"y":19.305993690851736}]},{"x":383.09148264984225,"y":19.305993690851736,"highlight":true,"active":true,"lines":[{"x":384.1009463722397,"y":19.305993690851736}]},{"x":384.1009463722397,"y":19.305993690851736,"highlight":true,"active":true,"lines":[{"x":384.1009463722397,"y":18.296529968454266}]},{"x":384.1009463722397,"y":18.296529968454266,"highlight":true,"active":true,"lines":[{"x":385.1104100946372,"y":25.3627760252366}]},{"x":385.1104100946372,"y":25.3627760252366,"highlight":true,"active":true,"lines":[{"x":385.1104100946372,"y":26.37223974763407}]},{"x":385.1104100946372,"y":26.37223974763407,"highlight":true,"active":true,"lines":[{"x":386.11987381703466,"y":27.381703470031553}]},{"x":386.11987381703466,"y":27.381703470031553,"highlight":true,"active":true,"lines":[{"x":386.11987381703466,"y":29.400630914826507}]},{"x":386.11987381703466,"y":29.400630914826507,"highlight":true,"active":true,"lines":[{"x":388.13880126182966,"y":29.400630914826507}]},{"x":388.13880126182966,"y":29.400630914826507,"highlight":true,"active":true,"lines":[{"x":388.13880126182966,"y":30.410094637223978}]},{"x":388.13880126182966,"y":30.410094637223978,"highlight":true,"active":true,"lines":[{"x":388.13880126182966,"y":32.42902208201893}]},{"x":388.13880126182966,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":389.1482649842271,"y":32.42902208201893}]},{"x":389.1482649842271,"y":32.42902208201893,"highlight":true,"active":true,"lines":[{"x":389.1482649842271,"y":33.4384858044164}]},{"x":389.1482649842271,"y":33.4384858044164,"highlight":true,"active":true,"lines":[{"x":391.16719242902207,"y":33.4384858044164}]},{"x":391.16719242902207,"y":33.4384858044164,"highlight":true,"active":true,"lines":[{"x":391.16719242902207,"y":35.45741324921137}]},{"x":391.16719242902207,"y":35.45741324921137,"highlight":true,"active":true,"lines":[{"x":391.16719242902207,"y":36.46687697160884}]},{"x":391.16719242902207,"y":36.46687697160884,"highlight":true,"active":true,"lines":[{"x":392.17665615141954,"y":37.47634069400631}]},{"x":392.17665615141954,"y":37.47634069400631,"highlight":true,"active":true,"lines":[{"x":393.186119873817,"y":38.48580441640378}]},{"x":393.186119873817,"y":38.48580441640378,"highlight":true,"active":true,"lines":[{"x":394.1955835962145,"y":39.49526813880128}]},{"x":394.1955835962145,"y":39.49526813880128,"highlight":true,"active":true,"lines":[{"x":394.1955835962145,"y":40.50473186119875}]},{"x":394.1955835962145,"y":40.50473186119875,"highlight":true,"active":true,"lines":[{"x":394.1955835962145,"y":41.51419558359622}]},{"x":394.1955835962145,"y":41.51419558359622,"highlight":true,"active":true,"lines":[{"x":395.20504731861195,"y":41.51419558359622}]},{"x":395.20504731861195,"y":41.51419558359622,"highlight":true,"active":true,"lines":[{"x":395.20504731861195,"y":42.52365930599369}]},{"x":395.20504731861195,"y":42.52365930599369,"highlight":true,"active":true,"lines":[{"x":395.20504731861195,"y":43.53312302839116}]},{"x":395.20504731861195,"y":43.53312302839116,"highlight":true,"active":true,"lines":[{"x":396.2145110410094,"y":46.5615141955836}]},{"x":396.2145110410094,"y":46.5615141955836,"highlight":true,"active":true,"lines":[{"x":397.22397476340694,"y":47.57097791798107}]},{"x":397.22397476340694,"y":47.57097791798107,"highlight":true,"active":true,"lines":[{"x":397.22397476340694,"y":48.58044164037857}]},{"x":397.22397476340694,"y":48.58044164037857,"highlight":true,"active":true,"lines":[{"x":399.2429022082019,"y":50.59936908517351}]},{"x":399.2429022082019,"y":50.59936908517351,"highlight":true,"active":true,"lines":[{"x":400.25236593059935,"y":50.59936908517351}]},{"x":400.25236593059935,"y":50.59936908517351,"highlight":true,"active":true,"lines":[{"x":400.25236593059935,"y":51.60883280757098}]},{"x":400.25236593059935,"y":51.60883280757098,"highlight":true,"active":true,"lines":[{"x":401.2618296529968,"y":51.60883280757098}]},{"x":401.2618296529968,"y":51.60883280757098,"highlight":true,"active":true,"lines":[{"x":402.2712933753943,"y":52.61829652996845}]},{"x":402.2712933753943,"y":52.61829652996845,"highlight":true,"active":true,"lines":[{"x":403.28075709779176,"y":52.61829652996845}]},{"x":403.28075709779176,"y":52.61829652996845,"highlight":true,"active":true,"lines":[{"x":401.2618296529968,"y":48.58044164037857,"highlight":true,"active":true,"lines":[{"x":401.2618296529968,"y":49.58990536277604}]}]}],"textBox":{"active":false,"hasMoved":false,"movesIndependently":false,"drawnIndependently":true,"allowedOutsideImage":true,"hasBoundingBox":true,"x":488.07570977917976,"y":337.2870662460568,"boundingBox":{"width":182.2578125,"height":26,"left":483.49999999999994,"top":417}},"invalidHandlePlacement":false},"uuid":"409ad544-02dd-487f-8f4c-91a2c5601afb","canComplete":false,"highlight":false,"polyBoundingBox":{"left":118.61198738170346,"top":18.296529968454266,"width":369.4637223974763,"height":637.9810725552051},"area":136311.35746201072}]}}';
  // --- To put the tool data back ---
  var allToolData = JSON.parse(toolDataString);
  for (var toolType in allToolData) {
    if (Object.prototype.hasOwnProperty.call(allToolData, toolType)) {
      for (var i = 0; i < allToolData[toolType].data.length; i++) {
        var toolData = allToolData[toolType].data[i];
        cornerstoneTools.addToolState(element, toolType, toolData);
      }
    }
  }
  // Update the canvas
  cornerstone.updateImage(element);
};

onMounted(() => {
  setTimeout(() => {
    init();
    const FreehandRoiTool = cornerstoneTools.FreehandRoiTool;
    const ZoomTool = cornerstoneTools.ZoomTool;
    const BrushTool = cornerstoneTools.BrushTool;

    const element = document.getElementById("dicomImage");
    document
      .getElementById("downloadAndView")
      .addEventListener("click", function (e) {
        console.log(e);
        const url = document.getElementById("wadoURL").value;

        // image enable the dicomImage element and activate a few tools
        cornerstone.enable(element);
        cornerstone.loadImage(url).then(function (image) {
          cornerstone.displayImage(element, image);
          const toolState = {};
          cornerstoneTools.addToolState(element, "myToolState", toolState);
          cornerstoneTools.addTool(FreehandRoiTool);
          cornerstoneTools.addTool(BrushTool);
          cornerstoneTools.addTool(ZoomTool, {
            // Optional configuration
            configuration: {
              invert: false,
              preventZoomOutsideImage: false,
              minScale: 0.1,
              maxScale: 20.0,
            },
          });

          cornerstoneTools.setToolActive("Zoom", { mouseButtonMask: 2 });
          cornerstoneTools.setToolActive("FreehandRoi", { mouseButtonMask: 1 });
          loaded.value = true;
        });
      });
  }, 500);
});

watch(
  () => selectedTool.value,
  () => {
    cornerstoneTools.addTool(selectedTool.value.enableValue);
    cornerstoneTools.setToolActive(selectedTool.value.value, {
      mouseButtonMask: 1,
    });
    // cornerstoneTools.setToolActive(selectedTool.value, { mouseButtonMask: 1 });
    // console.log(selectedTool.value, "selectedTool.value");
  }
);
</script>

<style lang="scss">
.ccanvas {
  height: 100%;
  color: white;
  position: relative;
  border-style: solid;
  border-color: black;
  display: inline-block;
  width: calc(100vw - 650px);
  height: calc(100vh - 100px);
}
.dicom-image {
  color: white;
  border: 1px solid red;
  position: relative;
  display: inline-block;
  height: calc(100vh - 100px);
  width: calc(100vw - 650px);
}
</style>
