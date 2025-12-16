<script lang="ts">
  import "./style.css";
  import type { ResultTemplateData } from "$lib/types/rusult";
  import ResultHeader from "./ResultHeader.svelte";
  import StudentInfo from "./StudentInfo.svelte";
  import RecordsTable from "./RecordsTable.svelte";
  import ScoreSummary from "./ScoreSummary.svelte";
  import StudentRatings from "./StudentRatings.svelte";
  import TeacherRemark from "./TeacherRemark.svelte";

  interface Props {
    data: ResultTemplateData["data"];
  }

  let { data }: Props = $props();

  // Check if student type is GRADERS to conditionally show ratings
  const isGraders = $derived(data.student.category === "GRADERS");
</script>

<div class="w-full h-full bg-custom">
  <!-- Header Section -->
  <ResultHeader school={data.school} />

  <!-- Student Info Section -->
  <StudentInfo student={data.student} />

  <!-- Records Table -->
  <RecordsTable records={data.records} student={data.student} />

  <!-- Score Summary -->
  <ScoreSummary score={data.score} student={data.student} />

  <!-- Student Ratings (for GRADERS only) -->
  {#if isGraders && data.ratings.length > 0}
    <StudentRatings ratings={data.ratings} />
  {/if}

  <!-- Teacher's Remark -->
  <TeacherRemark remark={data.remark} />
</div>
