<script setup>
</script>

<template>
    <button class="cta-btn cta-btn--primary resumeButton" type="button">
        <!-- CV / Document icon -->
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="resume-icon">
            <path fill-rule="evenodd" d="M5.625 1.5c-1.036 0-1.875.84-1.875 1.875v17.25c0 1.035.84 1.875 1.875 1.875h12.75c1.035 0 1.875-.84 1.875-1.875V12.75A3.75 3.75 0 0 0 16.5 9h-1.875a1.875 1.875 0 0 1-1.875-1.875V5.25A3.75 3.75 0 0 0 9 1.5H5.625ZM7.5 15a.75.75 0 0 1 .75-.75h7.5a.75.75 0 0 1 0 1.5h-7.5A.75.75 0 0 1 7.5 15Zm.75 2.25a.75.75 0 0 0 0 1.5H12a.75.75 0 0 0 0-1.5H8.25Z" clip-rule="evenodd" />
            <path d="M12.971 1.816A5.23 5.23 0 0 1 14.25 5.25v1.875c0 .207.168.375.375.375H16.5a5.23 5.23 0 0 1 3.434 1.279 9.768 9.768 0 0 0-6.963-6.963Z" />
        </svg>
        <span class="btn-label">Resume</span>
    </button>
</template>

<style scoped>

/* ── Button Component — Fill / Primary pill ──
   Hover: gradient sweeps from right to left (purple slides in from right) */
.cta-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 7px;
    padding: 10px 24px;
    border-radius: 50px;
    font-family: var(--font-body);
    font-size: 15px;
    font-weight: 500;
    letter-spacing: 0.2px;
    cursor: pointer;
    border: none;
    outline: none;
    position: relative;
    overflow: hidden;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
    color: #fff;
}

.cta-btn--primary {
    /* Wide gradient (200%) — shift position on hover for sweep effect */
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    background-position: left center;
    box-shadow: 0 4px 18px rgba(108, 99, 255, 0.35);
    transition:
        background-position 0.55s ease,
        box-shadow          0.3s ease,
        transform           0.2s ease;
}

.cta-btn--primary:hover {
    background-position: right center;
    box-shadow: 0 8px 28px rgba(155, 89, 245, 0.55);
    transform: translateY(-2px);
}

.cta-btn--primary:active {
    transform: translateY(1px) scale(0.97);
    box-shadow: 0 3px 12px rgba(108, 99, 255, 0.3);
}

.resume-icon {
    width: 17px;
    height: 17px;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
}

.btn-label {
    position: relative;
    z-index: 1;
}

</style>